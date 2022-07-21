# dbdiff

- 对比 MySQL 结构和数据差异，并生成 SQL。
- 创建 Markdown 结构文档。
- 它是用 golang 编写的，可以在任何操作系统上构建和使用。

## 安装

1. 安装最新 golang. <https://golang.org/dl/>
2. 下载源码 `git clone https://github.com/jaksal/dbdiff.git`
3. 进入源码文件夹
4. 运行 `go get && go build`

## 使用

### 创建结构差异脚本

```
dbdiff -diff_type=schema
  -source="uid:pwd@tcp(server_ip:port)/dbname"
  -target="uid:pwd@tcp(server_ip:port)/dbname"  
  -output=output.sql
```

### 创建数据差异脚本 ( 要比较的表必须具有相同的结构才能正常工作。 )

```
dbdiff -diff_type=data
  -source="uid:pwd@tcp(server_ip:port)/dbname" 
  -target="uid:pwd@tcp(server_ip:port)/dbname" 
  -output=output.sql
```

### 创建 Markdown 结构文档 

```
dbdiff -diff_type=md
  -source="uid:pwd@tcp(server_ip:port)/dbname"
  -output=output.md
```

- 示例文件位于示例文件夹中。 
- 输出 md 文件转换为 pdf ==> ( https://github.com/jaksal/md2pdf )

### 创建 sql 结构脚本

```
dbdiff -diff_type=sql
  -source="uid:pwd@tcp(server_ip:port)/dbname"
  -output=output.sql
```

### 扩展选项

```
  -include="test_"    // include db object name containing test_  
  -exclude="test_"    // exclude db object name containing test_  
  -output="[DATE]/output.sql"   // create today date folder
  -ignore_column=update_date  // ignore column in data diff mode
```

## 问题

比较表的时候，如果只是改变了列名，单独用 sql 是无法知道的，所以去掉列，再增加一列。
请注意，在此过程中数据将丢失。
