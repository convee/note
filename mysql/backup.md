---
title: "Mysql 备份与恢复"
date: 2020-12-13
comments: false
tags: ["mysql"]
---
## 恢复到指定数据库
```
mysql -hhostname -uusername -ppassword databasename < backup.sql
```
## 还原压缩的MySQL数据备份文件
```
gunzip < backup.sql.gz | mysql -uusername -ppassword databasename
```
## 直接将备份导入到新的数据库
```
mysqldump -uusername -ppassword databasename | mysql -host=192.168.0.1 -C databasename
```
## 使用source导入sql文件
```
mysql > use test
mysql > source /data/test_backup.sql
```