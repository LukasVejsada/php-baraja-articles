PHPによるオブジェクト指向プログラミング入門
=======================

> id: '44a79461-dcfd-4dd0-b6fd-ba5db76db6de'
> slug:
> 	cs: uvod-do-oop
> 	ja: phpniyoruobujekuto-zhi-xiangpuroguramingu-ru-men
> 
> publicationDate: '2020-01-01 19:54:35'
> mainCategoryId: '3e45c55a-a4cd-4745-b1bb-0332702fefbf'
> sourceContentHash: '888db2cf35845892eebade9fdcc18871'

オンラインコース「OOP in PHP」の第1回目の記事へようこそ。記事の全リストは<a href="/opp">概要ページ</a>をご覧ください。

> コンテンツに関する注意事項
>
> このシリーズの目標は、オブジェクト指向プログラミングのエッセンス**を**最もよく説明し、意味のないことに何百時間も実験する必要がないようにすることです。すべてのテクニックとチュートリアルは実践から得られたもので、私自身がプログラミングを学んでいたときに読みたかったように説明されています。というのも、プログラミングに没頭してすべてがめちゃくちゃになってしまうよりは、原理を中心に理解し、少なくとも問題点についてはある程度理解していたほうがいいと思うからです。
>
> すぐにわかるように、OOPでのプログラミングは、コードに大きなメリットをもたらします。アプリケーションに新しいレベルの抽象性をもたらし、他の方法では不可能な非常に複雑な問題を解決することができます。

オブジェクトとは
------------------

プログラミングの基本概念において、オブジェクトとは、自身の値に加えて、現実世界と同じように詳細な状態やメソッド、動作を定義し、様々な操作を行うことができる特別なデータ型のことである。

プログラミングにおけるオブジェクトとは、現実世界の「モノ」のように名前を付けることができ（例えば名詞で）、現実世界のモノのような特性を持つものである。例えば、オブジェクトは、いくつかの値（タイトル、コンテンツ、著者、出版日、...）とメソッド（新しいタイトルの挿入、コンテンツの読み込み、出版からの日数の計算、...）を持つ記事とすることができます。今回は、主にオブジェクトの作成方法と基本的な操作方法を扱います。

オブジェクトとクラス
---------------

すでに述べたように、**オブジェクトは存在するもの**です。この段階では、「存在する」という言葉が非常に重要です。なぜなら、すぐにわかるように、プログラミングで扱うべき実用的な実装がまだ残っているからです。

プログラミングではコードを書き、オブジェクトは「生きている」ものなので、ここからは、意味を詳細に理解し、これを厳密に区別することが重要な2つの異なる概念を区別することにします。

- オブジェクト**とは、今現在存在する（インスタンスを持つ）「生きている」ものであり、何かを実行したり、他のオブジェクトに反応したりすることができます。
- クラス**は、まだ評価されていない静的に書かれたコードで、ずっと同じままです。

プログラミングでは常に静的な文字列（テキスト）としてコードを書くので、プログラムを`クラス`（オブジェクト全体の静的な定義）と`オブジェクト`（クラスの`生きた`インスタンス）に区別することにします。

クラス定義の例です。

```php
class Article
{
    public string $title;

    public ?string $autor = null;
}
```

> **実用上の注意事項：**.
>
> 実際のアプリケーションでは、各クラスは通常別の PHP ファイルに書き込まれ、そのファイル名はクラス名と同じになります。
>
> そこで、例えば `Article` クラスでは、`src/Article.php` を作成します。この規約は PHP では必須ではありませんが、アプリケーションを読みやすくするために、たくさんのコードが一か所にまとまっていないようにするために役立ちます。
>
> 各クラスはアプリケーション全体で最大1つしか存在できませんが（ユニークな名前を持つ）、インスタンスは（RAM容量に依存して）ほぼ無限に存在することが可能です。さらに、一つのクラスを複数のファイルに分割することはできず、一度に一箇所で定義する必要があります。同じ名前のクラスを複数作成する必要がある場合は、**名前空間**を使用します。
>
> また、よく構造化されたコードは、多くのプロジェクトで再利用できることを後で紹介します。

このコードでは、2 つのプロパティ (`title` と `author`) を持つ `Article` クラスを定義しています。 PHP はコメントを無視し、静的な型チェック (通常は PhpStorm が読み取る) にのみコメントを使用します。

コード

```php
public string $title;
```

は `properties` の定義を意味し、これは `Article` クラスのプロパティです。これは、`Article`が一種のフィールドで、`title`がそのインデックスであり、そこに値を書き込むことができると考えることができます。各プロパティには、定義されたアクセシビリティ (`public`、`protected` または `private`) が必要です。それぞれの設定の意味については、後ほど説明します。もし、特定のケースでどのアクセシビリティを選択したらよいかわからない場合は、 `public` と書いてください。

クラスのインスタンス化とオブジェクトの生成
----------------------------------

インスタンス`の概念は、理解するのが最も難しい概念の1つです。したがって、以下の行を注意深く読むことが重要であり、すべての例を公平に試してみることをお勧めします。

もしアプリケーションがソースコードの中ですでにクラスを定義していたとしても、 それは実際にはどこにも使われておらず、PHP はそのクラスについて知ることはありません。これは、OOPが「データのカプセル化の原則」を導入しているためで、クラスはそのクラスの内部でのみ有効な内部（ローカル）コンテキストを持つことを意味します。これは、オブジェクトレス開発では、常にコード全体を評価することに慣れていたためです。また、クラスは何らかの関数や外部から呼び出されるプログラムであると考えるようにしてください。

ここで、最初のインスタンスを作成します。その際、 `new` 演算子を使用します。

```php
$myArticle = new Article;
$myArticle->title = '初めての記事'; // 値を書き込む

echo $myArticle->title; // "初めての記事 "を掲載
```

new` 演算子によって作られた `Article` オブジェクト全体を `$myArticle` 変数に格納することに注意してください。これは、オブジェクトが実際には `データ型` であることを意味し、変数間で移動して作業を継続することができます。

オブジェクトを操作するには `->` 矢印演算子を使用します。特定のオブジェクトのインスタンスがあれば（その中身を変数として持っていれば）、内部のプロパティに値を書き込んだり、メソッド（後述）を使って読み込んだり、様々な方法で変更することが簡単にできるのです。

オブジェクトの**インスタンスは、メモリ内にクラスのローカルな「ライブ」コピー（変数）を作成することです**。

同じクラスのインスタンスを同時に複数作成すること
---------------------------------------------

すでに説明したように、各オブジェクトはその内部で適用されるローカルコンテキストを持っています。この原理を利用すれば、同じクラスの独立したインスタンスを多数作り、自由に操作することができる。動的な数のインスタンスを作成し、例えば配列の要素として格納することも可能です。可能性は無限大です。

> **警告:**
>
> 極めて多数のインスタンス(数百以上)を作成する場合、PHPはすべてのインスタンスに関する情報をRAMに保持する必要があるため、メモリのフットプリントに留意してください。しかし、実際には、多数のインスタンスによってメモリがオーバーフローする問題は発生しない。

例

```php
$firstArticle = new Article;
$firstArticle->title = '初めての記事';

$secondArticle = new Article;
$secondArticle->title = '犬と猫について';

echo $firstArticle->title;  // "初めての記事 "を掲載
echo $secondArticle->title; // "犬と猫について "を書き出す
```

title` (`->title`) プロパティのリストは、どのインスタンスから読み込んでいるかに依存することに注意してください。

概要
-------

ここまで、最初のクラスを定義し、そのインスタンス（オブジェクト）を作成して、そこにいくつかの値を書き込む方法を紹介しました。

次回は、<a href="/methods-and-passing-input">Constructor, Methods and Passing Input</a>の概念について説明します。