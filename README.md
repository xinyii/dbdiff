dbdiff
======

[中文说明](./README_CN.md)

- create mysql schema and data diff script.
- create markdown schema document.

It is a tool to compare mysql databases and extract schema and data changes to sql.

There is also a function to generate schema documents as md files.

It is written in golang and can be built and used on any OS.

install :
-------------

* install golang latest. (https://golang.org/dl/)
* download src (git clone https://github.com/jaksal/dbdiff.git)
* goto src folder 
* go get && go build

usage :
-------------

* create schema diff script

```
dbdiff -diff_type=schema
  -source="uid:pwd@tcp(server_ip:port)/dbname"
  -target="uid:pwd@tcp(server_ip:port)/dbname"  
  -output=output.sql
```

* create data diff script ( The table to be compared must have the same schema to work properly. )

```
dbdiff -diff_type=data
  -source="uid:pwd@tcp(server_ip:port)/dbname" 
  -target="uid:pwd@tcp(server_ip:port)/dbname" 
  -output=output.sql
```

* create markdown document 

```
dbdiff -diff_type=md
  -source="uid:pwd@tcp(server_ip:port)/dbname"
  -output=output.md
```
-- The sample files are in the sample folder. 
-- output md file convert to pdf ==> ( https://github.com/jaksal/md2pdf )

* create sql script

```
dbdiff -diff_type=sql
  -source="uid:pwd@tcp(server_ip:port)/dbname"
  -output=output.sql
```

* extra option

```
  -include="test_"    // include db object name containing test_  
  -exclude="test_"    // exclude db object name containing test_  
  -output="[DATE]/output.sql"   // create today date folder
  -ignore_column=update_date  // ignore column in data diff mode
```

* bug

When comparing tables, if only the column name has been changed, it cannot be known with sql alone, so drop the column and add a new one.
Please note that data will be lost during this process.
