## 如何查找进程，查找端口被占用的原因？
* 找出 php-fpm 进程
```shell
ps aux | grep php-fpm
```

## 找出ssh端口 
```
lsof -i -P | grep ssh 
```

##  找出22端口占用的原因
```
lsof -i -P | grep :22
```
> 如果lsof不存在，联系管理员安装，安装命令yum install -y lsof

## 查看进程数
```
pstree | grep mysql
```

## 如何查找文件、目录、程序安装目录的位置？以及文件及文件夹的基本操作（创建、删除、复制、打包，解压缩）
* 找出执行程序的位置，如果在标准path路径下面，可以用
```
whereis docker
```

* 在当前目录及子目录下面搜索文件 
```
find . -type f | grep docker
```

* 快速创建一个文件 
```
touch test.txt
```

* 拷贝一个文件
```
cp test.txt new.txt
```

* 拷贝文件夹，可以用 
```
rsync -avzP src_dir/ dest_dir
```

> 第一个参数是源文件夹，记得加/，不然拷贝就是把这个目录放到目标目录的下面去 了（成为子目录了）

* 比较两个目录结构 
```
tree src_dir dest_dir
```

* 压缩目录  
```
tar zcvf src.tgz src_dir
```

> 第一个参数是目标.tgz文件， 第二个参数是要打包的源文件夹

* 删除目录或者文件
```
rm -rf src_dir 
```

> -rf表示强制，并递归删除，src_dir是要删除的目录

* 解压文件 
```
tar zxvf src.tgz
```

## 如何查看机器运行的建康指标，如：CPU的LOAD和使用率，内存使用率，磁盘使用率，IOWAIT等，除此之外还有那些重要指标可以用来分析特定场景问题？
> yum install iotop iftop iostat htop 安装一系列工具 htop是top命令的加强版，可以看到cpu，内存，执行的进程等信息

* iftop 是监控网卡的
* iotop 是监控io的
* free -m 监控可用内存
* uptime 查看当前系统负载
* df -hl 查看磁盘
* 安装smart 工具yum install -y smartmontools,查看磁盘的smart信息smartctl -a /dev/sda
* 查看cpu信息cat /proc/cpuinfo
* 查看内存信息 cat /proc/meminfo



