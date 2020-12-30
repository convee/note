---
title: PHP Redis 扩展安装
date: '2020-12-13T00:00:00.000Z'
comments: false
tags:
  - php
  - redis
---

# PHP Redis 扩展安装

## 下载源码

```text
wget https://github.com/phpredis/phpredis/archive/5.3.2.tar.gz
```

## 解压

```text
tar -zxvf 5.4.3.tag.gz
```

## 进入源码目录

```text
cd phpredis-5.3.2
```

## 侦测环境

* 并生成相应的配置文件（包括 configure）phpize 为当前环境下的命令，与 php 是同一级别的

  ```text
  /usr/local/php7/bin/phpize
  ```

  **检查配置与依赖**

  ```text
  ./configure [--enable-redis-igbinary] [--enable-redis-msgpack] [--enable-redis-lzf [--with-liblzf[=DIR]]] [--enable-redis-zstd]
  ```

  **编译**

* 会在 modules 目录下生成 redis.so 文件，
* 复制到 extension\_dir 目录下，扩展会成功

  ```text
  make
  ```

  **安装**

  ```text
  make install
  ```

  **phpredis 文档**

  [https://github.com/phpredis/phpredis/blob/develop/INSTALL.markdown](https://github.com/phpredis/phpredis/blob/develop/INSTALL.markdown)

