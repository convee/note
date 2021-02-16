## 查询日志中含有某个关键字的信息
```shell
cat app.log |grep 'error'
```


## 查询日志尾部最后10行的日志
```shell
tail  -n  10  app.log 
```

## 查询10行之后的所有日志
```shell
tail -n +10 app.log  
```

## 查询日志文件中的头10行日志
```shell
head -n 10  app.log  
```

## 查询日志文件除了最后10行的其他所有日志
```shell
head -n -10  app.log 	
```

## 查询日志中含有某个关键字的信息,显示出行号
```shell
cat -n  app.log |grep 'error'
```

## 显示102行,前10行和后10行的日志
```shell
cat -n app.log |tail -n +92|head -n 20
```

## 根据日期时间段查询
```shell
sed -n '/2014-12-17 16:17:20/,/2014-12-17 16:17:36/p'  app.log
```

## 使用more和less命令(分页查看,使用空格翻页)
```shell
 cat -n app.log |grep "error" |more
 ```

## 把日志保存到文件
```shell
cat -n app.log |grep "error"  > temp.txt
```