## 安装依赖包

```
yum install -y gcc gcc-c++  make zlib zlib-devel pcre pcre-devel  libjpeg libjpeg-devel libpng libpng-devel freetype freetype-devel gdbm-devel db4-devel libXpm-devel libX11-devel gd-devel gmp gmp-devel expat-devel libxml2 libxml2-devel glibc glibc-devel glib2 glib2-devel bzip2 bzip2-devel ncurses ncurses-devel libcurl libcurl-devel curl curl-devel libmcrypt libmcrypt-devel libxslt libxslt-devel xmlrpc-c xmlrpc-c-devel libicu-devel libmemcached-devel libzip readline readline-devel e2fsprogs e2fsprogs-devel krb5 krb5-devel openssl openssl-devel openldap openldap-devel nss_ldap openldap-clients openldap-servers
```
## 下载 PHP

```
wget https://www.php.net/distributions/php-7.3.20.tar.gz
```
## 解压

```
tar -xzvf php-7.3.20.tar.gz
cd php-7.3.20
```
## 配置

```
./configure --prefix=/usr/local/php7 --with-config-file-path=/usr/local/php7/etc --enable-inline-optimization --disable-debug --enable-fpm --with-fpm-user=www --with-fpm-group=www --disable-rpath --enable-soap --with-libxml-dir --with-xmlrpc --with-openssl  --with-mhash --with-pcre-regex --with-zlib --enable-bcmath --with-bz2 --enable-calendar --with-curl --enable-exif --with-pcre-dir --enable-ftp --with-gd --with-openssl-dir --with-jpeg-dir --with-png-dir --with-zlib-dir --with-freetype-dir --enable-gd-jis-conv --with-gettext --with-gmp --with-mhash --enable-mbstring --with-onig --enable-shared --enable-opcache --with-mysqli=mysqlnd --with-pdo-mysql=mysqlnd --with-readline --with-iconv --enable-pcntl --enable-shmop --enable-sysvmsg --enable-sysvsem --enable-sysvshm --enable-sockets  --enable-zip --enable-wddx --with-pear
make && make install
```
## 创建www用户

```
groupadd www #添加 www 用户组
useradd -g www www #添加 www 用户到 www 用户组
```
## 初始化 php-fpm 配置

* 复制 php.ini
```
cp php-7.2.20/php.ini-production /usr/local/php/etc/php.ini
```
* 增加执行权限
```
chmod +x /etc/init.d/php-fpm
```
* 配置 php-fpm 文件
```
cd /usr/local/php7/etc/
cp php-fpm.conf.default php-fpm.conf
```
* 进入 php-fpm.conf , 并去除 pid = run/php-fpm.pid 的注释
 ```
vim php-fpm.conf
```
* 复制 www.conf 文件
```
cp php-fpm.d/www.conf.default php-fpm.d/www.conf
```
## php-fpm 启动脚本
```
/etc/init.d/php-fpm stop # 停止服务
/etc/init.d/php-fpm start # 启动服务
/etc/init.d/php-fpm restart # 重启服务
```
* 复制启动脚本到 init.d 目录
```
cp php-7.2.20/sapi/fpm/init.d.php-fpm /etc/init.d/php-fpm
```
## centos 管理服务化
```
systemctl enable xxxxxx # 配置自启动
systemctl stop xxxxx # 停止服务
systemctl start xxxx # 开启服务
systemctl status xxxx # 查看状态
```
* 在 centos 7 之后我们可以使用 systemctl 更好的管理系统服务
* 所以我们也要让 php-fpm 支持
* 因为 php 7.2 源码包里面含有 systemctl 所需要的脚本文件
* 我们只要复制过去即可,我们来开始配置
* 进入下载的 php源码包
```
cd php-7.2.20/sapi/fpm
```
* 复制其中的 php-fpm.service 到 /usr/lib/systemd/system/
```
cp php-fpm.service /usr/lib/systemd/system/
```
* 再次使用 systemctl enable php-fpm 进行配置自启动
```
systemctl enable php-fpm
```
* 重启测试一下看看自己服务器的 php-fpm 是否成功运行
## php别名设置
* 新增 /usr/bin/php 文件
* chmod u+x /usr/bin/php
* ln -s /usr/local/php7/bin/php /usr/bin/php