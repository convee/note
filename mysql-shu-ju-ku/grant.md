---
title: Mysql 创建用户与授权
date: '2020-12-13T00:00:00.000Z'
comments: false
tags:
  - mysql
---

# Mysql 创建用户与授权

### 命令:

```text
CREATE USER 'username'@'host' IDENTIFIED BY 'password';
```

### 说明：

* username：用户名
* host：用户可以登录的主机
* password：用户登录密码，密码可以为空

  **例子：**

  ```text
  CREATE USER 'convee'@'localhost' IDENTIFIED BY '123456';
  CREATE USER 'convee'@'192.168.0.1_' IDENDIFIED BY '123456';
  CREATE USER 'convee'@'192.168.%.%' IDENTIFIED BY '123456';
  CREATE USER 'convee'@'%' IDENTIFIED BY '123456';
  CREATE USER 'convee'@'%';
  ```

  **授权:**

  **命令:**

  ```text
  GRANT privileges ON databasename.tablename TO 'username'@'host'
  ```

  **说明:**

* privileges：用户的操作权限，如SELECT，INSERT，UPDATE等，如果要授予所的权限则使用ALL
* databasename：数据库名
* tablename：表名，如果要授予该用户对所有数据库和表的相应操作权限则可用_表示，如_.\*

  **例子:**

  ```text
  GRANT SELECT, INSERT ON test.user TO 'convee'@'%';
  GRANT ALL ON *.* TO 'convee'@'%';
  ```

  **注意:**

* 用以上命令授权的用户不能给其它用户授权，如果想让该用户可以授权，用以下命令:

  ```text
  GRANT privileges ON databasename.tablename TO 'username'@'host' WITH GRANT OPTION;
  ```

  **设置与更改用户密码**

  **命令:**

  ```text
  SET PASSWORD FOR 'username'@'host' = PASSWORD('newpassword');
  ```

  如果是当前登陆用户用:

  ```text
  SET PASSWORD = PASSWORD("newpassword");
  ```

  **例子:**

  ```text
  SET PASSWORD FOR 'convee'@'%' = PASSWORD("123456");
  ```

  **撤销用户权限**

  **命令:**

  ```text
  REVOKE privilege ON databasename.tablename FROM 'username'@'host';
  ```

  **说明:**

* privilege, databasename, tablename：同授权部分

  **例子:**

  ```text
  REVOKE SELECT ON *.* FROM 'convee'@'%';
  ```

  **删除用户**

  **命令:**

  ```text
  DROP USER 'username'@'host';
  ```

