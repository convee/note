## 下载源码
```
wget https://github.com/phpredis/phpredis/archive/5.3.2.tar.gz
```
## 解压
```
tar -zxvf 5.4.3.tag.gz
```
## 进入源码目录
```
cd phpredis-5.3.2
```
## 侦测环境
* 并生成相应的配置文件（包括 configure）phpize 为当前环境下的命令，与 php 是同一级别的
```
/usr/local/php7/bin/phpize
```
## 检查配置与依赖
```
./configure [--enable-redis-igbinary] [--enable-redis-msgpack] [--enable-redis-lzf [--with-liblzf[=DIR]]] [--enable-redis-zstd]
```
## 编译
* 会在 modules 目录下生成 redis.so 文件，
* 复制到 extension_dir 目录下，扩展会成功
```
make
```
## 安装
```
make install
```
## phpredis 文档
https://github.com/phpredis/phpredis/blob/develop/INSTALL.markdown