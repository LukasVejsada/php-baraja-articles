スーパーグローバル変数
===========

> id: bc2107ee-6551-4559-8c02-9cecdf98d33b
> slug:
> 	cs: superglobalni-promenna
> 	ja: supagurobaru-bian-shu
> 
> publicationDate: '2019-11-01 09:29:46'
> mainCategoryId: '0e39aee9-2818-480c-8081-e0c2d039bb24'
> sourceContentHash: '792e217f1331f38ed0719d7abeb05e67'

スーパーグローバル変数は、グローバルなアプリケーションの状態やHTTP通信を渡すために使用されます。

これらの変数の主な利点は、いつでもどこでも利用可能であることです。実際には、インデックスによって特定の情報にアクセスする、値の配列である。異なる文脈では、鍵の利用可能性は異なる場合がある（以下に説明）。

スーパーグローバル変数の種類
--------------------------------

PHP のスーパーグローバルはすべて配列で、ドル記号の後にアンダースコア (`$GLOBALS` 以外) と大文字を続けたもので表されます。

PHP 7`では、特に次のようなものがあります。

| 変数名｜説明
|-------------|-------|
| `$_GET` ｜ GETメソッドで送られるURLパラメータ <a href="/methods-odesilani-dat"></a
| `$_POST` ｜ フォームデータ <a href="/methods-odesilani-dat">sent by POST</a> を送信します。<a href="/ajax-post">ajaxでは動作が異なる場合がある</a>ことに注意してください。
| `$_REQUEST` ｜任意のメソッド (`$_GET`, `$_POST`, `$_REQUEST`) で送信されたフォームデータ。
| 例えば `<input type="file">` のような構成で、現在アップロードされているファイルに関する技術的な情報を提供します。
| $_SERVER` | <a href="/info">Web サーバー設定</a>, IP アドレス, 設定...環境によって異なります (Terminal から PHP スクリプトを呼び出した場合、異なる値が含まれ、例えば現在のリクエストに関する情報が欠落します)。
| `$_COOKIE` | <a href="/cookies">cookies</a>を設定します。
| `$_SESSION` ｜ セッションデータ (<a href="/sessions">session</a>) が存在し、過去に設定されていた場合。
| `$GLOBALS` | **Warning, it doesn't contain an underscore in the name!** これはいわゆる <a href="global-variable">global-variable</a> で、キーワード `global` の代替表記法である。アプリケーションにグローバル変数 `$variable` がある場合、 `$GLOBALS["variable"]` 構造体を使用してアクセスすることもできます。しかし、グローバル変数の使用は、設計上、悪い不純な解決策なので、やらない方がいいでしょう。
| `$_ENV` ｜ PHP が動作している現在の環境についての情報。

既存の値をすべてリストアップするのは簡単です。

```php
foreach ($_SERVER as $key => $value {
	echo $key . ':' . $value . '<br>。';
}
```

> 注意: すべてのインデックスが常に存在しなければならないわけではありません (たとえば、スクリプトがCLIモードでcronを実行した場合、ページのURLやリクエストのIPアドレスを持つインデックスは存在しません)。

変数へのアクセス
-------------------

すべてのグローバル変数（`$_SESSION`を除く）は読み取り専用にすることをお勧めします。これは、グローバルなアプリケーションデータを含んでおり、他のコードがこれを考慮する可能性があるためです（例えば、インストールされた別のライブラリなど）。

グローバルステートのもう一つの欠点は、たとえ存在しても正確な値に頼れないことです。そのため、常に `isset()` 構造体でそのキーをチェックしなければなりません。

新しいクッキーを保存するには `setcookie()` を使用し、値を直接挿入しないでください。これは、読み取り専用であるためです。

教訓
-------

スーパーグローバル変数の値を盲目的に信用してはいけない!

ユーザーはURLと送信されるヘッダーを使用して、値がどのように設定されるかに影響を与えることができます。すべての入力は、常に慎重に検証されなければならない。

グローバルの登録 - 旧バージョンのPHPの問題点
------------------------------------------

古いバージョンの PHP (`5.4.0` まで) では、特別な `register-globals` ディレクティブ (`php.ini` で設定可能) があり、URL で渡されたすべてのパラメータを自動的に変数として登録するようになっていました。

例えば、こんな感じです。

あるユーザーが URL: `https://example.com/script.php?var=24` に到着した。

そして、PHPは自動的にスクリプト内に `$var` という変数に `24` という値を作成します。

だから、古典的にうまくいったのです。

```php
echo $var;
```

そのため、誰でも好きな変数をスクリプトに入れ、その内容を変更することができる。もちろん、セキュリティは常に優先されるものではありませんでした。そうでもないんです。

その他の情報源
------------

より詳しい説明は、<a href="https://www.php.net/manual/en/language.variables.superglobals.php">公式マニュアル</a>をご覧ください。