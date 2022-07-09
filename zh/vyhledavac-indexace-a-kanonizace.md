互联网搜索引擎的算法 - 索引和规范化
===================

> id: daa97e66-e77f-4741-ade2-905c1cfdbd56
> slug:
> 	cs: vyhledavac-indexace-a-kanonizace
> 	zh: hu-lian-wang-sou-suo-yin-qing-de-suan-fa-suo-yin-he-gui-fan-hua
> 
> publicationDate: '2016-09-11 11:00:00'
> mainCategoryId: '367f936c-073f-44bd-b399-30738e93137a'
> sourceContentHash: d73a30f413e4b8b77dbceda60b3cf173

在今天的课程中，我们将看一下互联网上的索引和规范化文件。

编制索引
--------

索引过程是由一个称为索引器的组件执行的。这是一个专门设计的程序，将下载的数据（爬虫下载的数据）变成一种特殊的数据类型，用于搜索--桶。

索引的问题是，你不能 "聪明地 "浏览文件，但顺序阅读（从头到尾阅读整个文本）是不可避免的，所以这是一门要求很高的学科，搜索引擎使用最强大的服务器来进行这项活动。在搜索过程中，没有其他任务像索引那样要求高，纯文本变成索引。

以从维基百科上下载的一个关于猫的页面为例。索引器得到页面的完整文本，必须去除不必要的东西（例如用户控制菜单、广告、页脚......），并解析页面以获得纯文本。例如，该文本可以是。

> 家猫（Felis silvestris f. catus）是野猫的一种驯化形式，几千年来一直是人类的伴侣。和它的野生亲戚一样，它属于小猫亚科，是该类动物的典型代表。它的身体轻巧，肌肉发达，完全适应于狩猎，爪子和牙齿锋利，视力、听力和嗅觉都很好。

摘自【维基百科】（http://cs.wikipedia.org/wiki/Ko%C4%8Dka_dom%C3%A1c%C3%AD）。

搜索引擎现在从文本中解析出单个单词，并将其写入单个桶中。然而，它不能直接进行写桶（主要是因为每个桶都存在许多副本，而且还会干扰搜索），所以它创建了一个关于未来桶应该是什么样子的要求清单，并将这些要求存储在临时存储器中。在我们的例子中，这样的列表可能是这样的（一些不重要的词可以被忽略或标记为停止词）。

| 文档ID | Word | 位置 | 类型 |
|--------------|-------|--------|-----------|
| 1 | 猫 | 1 | 正常 |
| 1 | 国内 | 2 | 正常 |
| 1 | 菲利斯 | 3 | 正常 |
| 1 | Is | 7 | StopWord |
| 1 | 驯养的| 8 | 正常的 |

这样的列表是巨大的（比原始文本大得多），但搜索起来还是比较快的，因为我们不必按顺序阅读所有的文本，而是可以按每一列的索引进行搜索，而且一页中的词被一个接一个地排成行。

在一段时间过去后（或完成了一些文件的数量），索引器停止工作，建立这个请求列表（为未来的桶），并开始再次读取数据，重建各个桶（这个列表包括已经工作的桶中的旧记录）。如果从已知的地址添加新的记录，这个过程将更新它们，而对于新的文件，它将包括它们。

这样，索引器将再次浏览列表，并慢慢地创建包含所有元素的新桶（它们看起来与前面章节中的例子相同），当所有的桶都完成后，它们将被发送到各个搜索服务器。在服务器上更新木桶是很耗时的（主要是由于大量的数据被移动），所以在这个操作期间，服务器是不可用的，数据在不同的时间在不同的服务器上更新。这导致，例如，一些用户可能得到不同的结果，因为每个用户在不同的配药服务器上搜索（由于负载分解）。一旦更新完成，一切都会恢复正常，所有用户都能平等地找到所有文件。

索引过程对每个搜索引擎都很重要，而做得最频繁、最仔细的是对互联网拥有最新看法的搜索引擎。谷歌每隔几个小时就进行一次这样的操作，Seznam每周一次（而且它的数据要少一百万倍）。

文件的规范化
--------------------

在全文搜索引擎的最初设计中，不需要任何类似规范化的东西，因为互联网是一个不断创造新内容的媒介。然而，随着时间的推移，重复现象（即同一内容出现在多个不同的URL上）已经出现，搜索引擎必须适应这种情况。一个典型的例子是维基百科，它有很多文章。其他网页的一些作者接管了这些文本（部分甚至全部），从而造成了重复。但在大多数情况下，这并不重要，因为源网页的排名（链接质量）比被剽窃的网页要高得多，但有时也会发生这种情况，即以牺牲盗版者的利益为代价降低原创者的地位。

搜索引擎不得不适应这种恶习，并创造了 "规范化 "一词，可以理解为从索引中 "删除 "某些页面。顺便说一句，这使得索引更小，搜索引擎不必不必要地一直抓取相同的内容。

每个搜索引擎内部都将重复的内容分为2大类。

自然重复
-------------------

这些都是由互联网的自然行为和它的特点造成的。

例如，URL`http://mathematicator.cz`可能与URL`http://www.mathematicator.cz`或`http://mathematicator.cz/index.php`具有相同的内容，因为这是标准的Apache服务器（以及一般的互联网）行为。

如果发现自然重复，搜索引擎会创建一个 "规范集"，这是一组页面，搜索引擎从中选择一个代表，在搜索中脱颖而出。如果一个链接通向canonical集的任何页面，其排名将自动传递给主要代表。

通常情况下，帮助搜索引擎创建这一套，并在网站上正确设置重定向是一个好主意，这将使搜索引擎更好地看待网站，主要代表将被更好地选择。

导致抄袭的重复内容
----------------------------

抄袭是当今互联网上的一个问题。 抄袭的存在本身并不重要，然而，用户对它特别感到困扰，因为他们不断发现相同的查询结果。你是否也曾发现一个查询有几个页面的文字完全相同？这正是搜索引擎试图防止的行为。

最大的问题是确定哪一页是原始来源--而且是通过机器来做。同样，搜索引擎将所有类似的页面放入一个规范集，并从该集中选择主要代表。如果来源是不同的领域，就不能把这种情况看成是自然重复（并选择任何候选者），而必须对所有页面进行定性评估，并客观地选择最好的一个--最好是内容的原始来源。

搜索引擎通常根据整个域名的排名和对某一文件的链接网络的强度来决定，但即使这样也是一种相当不可靠的方法。第二个因素通常也是文件的创建（索引）时间。因此，每个搜索引擎都会跟踪哪些页面经常产生新的内容，并经常访问这些页面，这样它最好能立即注意到新的页面，因此不会选择其他页面作为代理。

对这种选择方法的详细描述超出了本文的范围，可以成为整本书的主题。