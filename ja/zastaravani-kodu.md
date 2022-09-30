コードの陳腐化 - 互換性を維持する方法
====================

> id: '7837ee7e-a150-47bf-a338-2f4c03d5bbed'
> slug:
> 	cs: zastaravani-kodu
> 	ja: kodono-chen-fu-hua-hu-huan-xingwo-wei-chisuru-fang-fa
> 
> publicationDate: '2022-07-29 17:10:00'
> mainCategoryId: '3666a8a6-f2a3-405d-8263-bd53c4301fb3'
> sourceContentHash: '727b60c7258fb70e21b5acb445404db0'

複数のレイヤーや開発者が相互に通信する大規模なシステム（エンタープライズアプリケーション、共有ソフトウェアパッケージ、ライブラリなど）を開発する場合、新しいコードのバージョンをどのように扱うかという問題が発生する。

開発者のコミュニティのために、共有のComposerパッケージを開発したいという状況を例にとって見てみましょう。

セマンティックバージョニング
--------------------

後方互換性と前方互換性の問題を解決する前に、ソフトウェアの変更点をどのように把握するかを考える必要があります。現在（2022年）、すべての変更をバージョン管理する最良の方法は、Gitに入れることです。ソフトウェアのリポジトリは、例えばGitHubやGitLabで共有することができる。各ソフトウェアの変更には、各コミットを識別し、実際に何が起こったかを記述する一意の識別子があります。

私は、ライブラリを開発する際に、次のような戦略をとるとうまくいきました。

開発開始時には、`master` (または `main`) ブランチに最初のコミットが作成され、そこに基本的なファイル構造がコミットされます。

新しいリクエストごとに、master とは別のブランチが作成され、そこで作業することになります。変更の準備ができたら、マージリクエストを `Pull request` という形でマスターに送ります。リクエストに対してコードレビューが行われ、問題がなければ、その変更がマスターにマージされます。

ブランチに後方互換性のない変更 (BC break, `Back Compatibility Break` から) が含まれている場合、それに応じてマークを付けなければなりません。BCブレークの表記方法については、次章以降で説明する。

そして、次のような構造を持つタグを用いて、ライブラリの製品版にタグ付けを行います（**Semantic Versioning 2.0.0**に基づく）。

バージョン番号は `MAJOR.MINOR.PATCH` というフォーマットで記述します。バージョン番号のインクリメントは次のように行われる。

- MAJOR` - 他との後方互換性がない変更があった場合 (API)
- MINOR` - 後方互換性を維持したまま機能を追加する場合
- パッチ` - バグが修正され、後方互換性が維持されるとき

プレリリースを利用し、メタデータを付加することで、情報を絞り込むことが可能です。例えば、`1.0.0-alpha`、`1.0.1-beta+2`などです。

セマンティックバージョニングについては、公式サイト（https://semver.org）で詳しく紹介されています。

後方互換性と前方互換性
-------------------------------

ソフトウェアを設計する際には、常に**後方互換性**（新しい機能や変更は古いコードと互換性がなければならない）、場合によっては**前方互換性**（現在の機能は将来のインターフェース変更と互換性がなければならない）を考える必要があります。

この2つの作業を正しく行うことは、非常に難しいことです。互換性を壊さずに変更することは、常に可能とは限りません。

修正する場合は、常に段階的に進め、ユーザーが変更に対応するのに十分な時間を確保する必要があります。

以下の項では、その考え方について説明します。

ステージ1：非推奨の機能としてマークする
--------------------------------------

互換性の脅威の基本的なタイプは、過去に存在した機能の削除や名称変更です。多くの場合、これは関数が受け取る引数が変更されたか、または新しい方法では異なる方法で処理されるべき古いロジックであることが原因です。

第一段階では、コードの古い部分を非推奨とマークして、一切変更しないようにする必要があります。

PHP では、このために `@deprecated` というアノテーションがあり、 メソッド、関数、プロパティ、変数、定数、そして一般的に非推奨のコードすべての 上に直接記述する必要があります。

また、特定のものが非推奨である理由や、今後どのように変更されるかを書いておくとよいでしょう。例えば、新しい機能や使い方の名称を出す。

コードの陳腐化の実例。定数は削除されます。組み込みのEnumを使用する方が良いでしょう（新しいバージョンのPHPへの移行のため、BCが壊れます）。

```php
class OrderNotification
{
	/** 2022-05-24から非推奨、enum OrderNotificationTypeを使用 */。
	public const
		TYPE_EMAIL = '電子メール',
		TYPE_SMS = 'テキスト';
```

アノテーション `@deprecated` は、IDE（開発ツール）とコンパイルツールに対してのみ、無言の警告を発生させます。何も壊さない。

第2段階：新しいメソッド/ロジックを呼び出す
--------------------------------------

第二段階では、古い実装を新しい実装に置き換えますが、古い実装の中で新しい手法を使います。これにより、ユーザーに気づかれることなく、インターフェースの互換性を保つことができます。

例：代わりに新しい静的サービスが作成されたため、このメソッドは非推奨となりました。誰かが使えるので、非推奨とマークして、内部で新しい実装を呼び出すだけです。開発者は一般的に、この方式が将来的に完全に削除されることを想定しています。

```php
/** 2021-09-11 から非推奨 代わりに Ip::get() を使用します。*/
public static function userIp(): string
{
	return Ip::get();
}
```

フェーズ3：静的解析のためのアノテーションの変更
-------------------------------------------

PhpStan のような静的解析を使用している場合 (強く推奨します!) は、実際にデータ型を変更する前にまず PHPDoc のアノテーションを書き換えるのがよいでしょう。静的解析は、何かが壊れていることをユーザーに知らせますが、ランタイムはそのまま残ります。

ステージ4：通知書を捨てる
-----------------------

第4段階では、新しいメソッドが呼び出され、同時に `note` レベルのエラーがスローされます。アプリケーションはまだ動作しますが、ある機能が非推奨であり、変更または削除されるという情報をシステムログに徐々に保存し始めるだけです。今後は、このような変化に対して、積極的に注意喚起していく予定です。開発者は、開発中やコンパイル中にエラーを見ることになります。

```php
/** 2021-05-01から非推奨、代わりにUserMetaManagerを使用します。*/
public function getMeta(int $userId, string $key): ?string
{
	trigger_error(__METHOD__ . ': このメソッドは非推奨です。代わりにUserMetaManagerを使用してください。');
	return $this->userMetaManager->get($userId, $key);
}
```

ステージ5：例外を投げる
------------------------

メソッドを完全に削除する前に、致命的な例外のいずれかを投げることをお勧めします。特に、アプリケーションが完全に停止してしまうため、エラーを無視することはできません。コードを完全に削除するのとは異なり、実際に何が起こったのかをユーザーに通知するため、簡単にエラーを修正することができます。

ステージ6：コードの完全削除
-----------------------------

最終段階では、古いコードは完全に削除されます。もし、依存関係を修正していないユーザーがいれば、そのアプリケーションは壊れてしまいます。

センシティブなエリアでの重大なBCの破損は、常に次の`MAJOR`リリースで行われるべきで、少なくとも`MAJOR`リリースの1つ前に告知を投げることで指摘されるべきです。これをやらないと、ライブラリのアップデートが非常に難しくなります。