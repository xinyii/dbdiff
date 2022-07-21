dbdiff
======

- 创建 MySQL 结构和数据差异脚本。
- 创建 Markdown 模式文档。

它是一个比较 MySQL 数据库并将结构和数据更改提取到 sql 的工具。

还有一个功能可以将模式文档生成为 md 文件。

它是用 golang 编写的，可以在任何操作系统上构建和使用。

安装 :
-------------

* 安装最新 golang. (https://golang.org/dl/)
* 下载源码 (git clone https://github.com/jaksal/dbdiff.git)
* 进入源码文件夹
* go get && go build

使用 :
-------------

* 创建结构差异脚本

```
dbdiff -diff_type=schema
  -source="uid:pwd@tcp(server_ip:port)/dbname"
  -target="uid:pwd@tcp(server_ip:port)/dbname"  
  -output=output.sql
```

* 创建数据差异脚本 ( 要比较的表必须具有相同的结构才能正常工作。 )

```
dbdiff -diff_type=data
  -source="uid:pwd@tcp(server_ip:port)/dbname" 
  -target="uid:pwd@tcp(server_ip:port)/dbname" 
  -output=output.sql
```

* 创建 Markdown 文档 

```
dbdiff -diff_type=md
  -source="uid:pwd@tcp(server_ip:port)/dbname"
  -output=output.md
```
-- 示例文件位于示例文件夹中。 
-- 输出 md 文件转换为 pdf ==> ( https://github.com/jaksal/md2pdf )

* 创建 sql 脚本

```
dbdiff -diff_type=sql
  -source="uid:pwd@tcp(server_ip:port)/dbname"
  -output=output.sql
```

* 扩展选项

```
  -include="test_"    // include db object name containing test_  
  -exclude="test_"    // exclude db object name containing test_  
  -output="[DATE]/output.sql"   // create today date folder
  -ignore_column=update_date  // ignore column in data diff mode
```

* 问题

比较表的时候，如果只是改变了列名，单独用 sql 是无法知道的，所以去掉列，再增加一列。
请注意，在此过程中数据将丢失。
