PHP函数fopen()
============

> id: '733ba757-1d5f-4717-a088-5ddabe730838'
> slug:
> 	cs: fopen
> 	zh: php-han-shufopen
> 
> publicationDate: '2019-08-22 20:48:46'
> mainCategoryId: '0eeab3a7-a54b-46db-a253-ca6100145648'
> sourceContentHash: '6b791877e57d88840d603dea69967b69'

`fopen()`函数代表对磁盘上文件的低级访问。

程序员必须自己做所有的事情（打开文件，读取数据，写入新数据，关闭文件）。

如果你只是需要快速读写文件，还有更简单的选择。

- <a href="/file-get-contents">file_get_contents()</a> - 从一个文件中读取内容
- <a href="/file-put-contents">file_put_contents()</a> - 向一个文件写入内容

基本用途
----------------

```php
$text = '任何被保存的文本...';

$file = fopen('file.html', 'a+'); // 打开文件和模式

fwrite($file, $text); // 保存到文件
fclose($file);        // 关闭该文件
```

> 如果我们打开一个文件供阅读，而它没有被关闭，那么其他进程就不能访问它。

文件处理模式的类型
----------------------------

我们可以在不同的模式下处理文件，这些模式告诉我们关于访问权限的信息。

例如，如果我们想打开一个只读的文件，那么`r`模式就足够了。

如果我们打开文件进行写入，那么它将在磁盘上被标记为 "open"，另一个进程（脚本）将不能写入它，直到我们再次关闭它。这可以确保文件在写入过程中不会被破坏。

| 模式 | 意义 |
|-------|--------|
| 打开文件，如果它不存在，将被创建。
| `a+` | 打开一个文件，添加数据或读取数据，如果它不存在，将被创建。
| `r` | 打开只读 |
| | `r+` | 打开读和写 |
| `w` | 打开写入，原来的数据将被删除并被新的数据取代，如果不存在，将被创建。
| `w+` | 开启写和读，原来的数据将被删除并被新的数据取代，如果不存在，将被创建。