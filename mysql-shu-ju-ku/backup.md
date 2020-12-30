# Mysql 备份与恢复

## 恢复到指定数据库

```text
mysql -hhostname -uusername -ppassword databasename < backup.sql
```

## 还原压缩的MySQL数据备份文件

```text
gunzip < backup.sql.gz | mysql -uusername -ppassword databasename
```

## 直接将备份导入到新的数据库

```text
mysqldump -uusername -ppassword databasename | mysql -host=192.168.0.1 -C databasename
```

## 使用source导入sql文件

```text
mysql > use test
mysql > source /data/test_backup.sql
```

