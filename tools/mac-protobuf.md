# Mac 下使用 Protobuf2.6.1

### 1.安装 PHP
```bash
brew install php@7.3
```
### 2.安装 Protobuf 扩展
```bash
wget https://github.com/allegro/php-protobuf/archive/master.zip
 
unzip master.zip
 
cd php-protobuf-master
 
sudo /usr/local/opt/php@7.3/bin/phpize
 
sudo ./configure --prefix=/usr/local/opt/php@7.3/bin/php --with-php-config=/usr/local/opt/php@7.3/bin/php-config
 
make && make install
 
//然后在php.ini里面加一下extension = "protobuf.so"
```
### 3.安装 Composer
```bash
cd php-protobuf-master

curl -s http://getcomposer.org/installer | php

/usr/local/opt/php@7.3/bin/php composer.phar install
```
### 4. Protobuf 使用
```bash
/usr/local/opt/php@7.3/bin/php ./php-protobuf-master/protoc-gen-php.php test_km.proto
```
### 5. 附录
protocol buffers官方：[https://developers.google.com/protocol-buffers/?hl=zh-cn](https://developers.google.com/protocol-buffers/?hl=zh-cn)
protobuf github：[https://github.com/protocolbuffers/protobuf](https://github.com/protocolbuffers/protobuf)
