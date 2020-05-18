---
title: Windows环境下安装最新MySQL服务
comments: true
abbrlink: '0'
categories:
  - MySQL
tags:
  - MySQL
date: 2018-10-09 21:21:57
---

## 安装与配置

在开发领域我们存储数据一般都是使用专门的数据库服务器专门提供的数据库服务，如果需要让自己的机器也可以 提供数据库服务，那么就需要安装特定的数据库服务器软件，这种类型的软件也有很多：

- Oracle 

- MySQL 

- SQL Server

这里我们选择一个很常见的数据库服务器软件：MySQL
MySQL 的安装同样建议采用解压版（目的是了解那些自动安装过程都做了哪些事）

>下载地址：https://dev.mysql.com/downloads/mysql/

### 安装过程

1. 解压到纯英文路径 2

2. 解压目录添加 my.ini （可选）

>参考：
>
>http://www.cnblogs.com/Ray-xujianguo/p/3322455.html 
>
>https://gist.github.com/hanjong/1205199 
>
>https://dev.mysql.com/doc/refman/5.5/en/mysqld-option-tables.html

```mysql
[mysqld] 
# MySQL 安装目录 
	basedir=C:/Develop/mysql 
# 数据文件所在目录 
	datadir=C:/Develop/mysql/data

```

3.以管理员身份运行 CMD 执行以下命令，安装一个 MySQL 服务

```mysql
# 定位到安装目录下的 bin 文件夹 
$ cd <MySQL安装目录>/bin 
# 初始化数据所需文件以及获取一个临时的访问密码 
$ mysqld ‐‐initialize ‐‐user=mysql ‐‐console 
# 将 MySQL 安装为服务 可以指定服务名称 
$ mysqld ‐‐install MySQL

```

 4.登入 MySQL 服务器，重置密码

```mysql
# 先通过用户名密码进入 MySQL 操作环境 
$ mysql ‐u root ‐p 
Enter password: # 输入临时密码   
# 设置数据库访问密码，一定要加分号 
mysql> set password for 'root'@'localhost' = password('123456');

#这一步可能会报错 ERROR 1064 (42000) 提示SQL语法错误
#尝试这条命令
mysql> alter user 'root'@'localhost' identified by '123';
# 或
mysql> update mysql.user set authentication_string=password('123456') where user='root' and Host = 'localhost';
```

解释：上面可能会报错的原因是MySQL5.7.6版本以后，password属性已经取消（使用SELECT  Password）

![](http://pan.vmccc.cn/images/2018/10/09/0fWpIoI6N4/mysql-error1064.jpg)

![](http://pan.vmccc.cn/images/2018/10/09/RRArT1cL4q/mysql-error1820.jpg)

## 基础操作

### 数据库管理工具 

数据库管理工具本质上就是一个使用数据库服务器软件（Server）提供的服务的数据库客户端（Client）。

### 命令行工具 

一般如果只是简单操作数据库，推荐使用 MySQL 内置的命令行工具完成：

通过命令行运行解压目录下 bin 目录中的 mysql.exe ：

```mysql
# 定位到 bin 目录 
$ cd <解压目录>/bin 
# 运行 mysql，‐u 指定数据库用户名，‐p 指定密码 
$ mysql ‐u root ‐p wanglei 
# 一般不建议在命令中填写密码，因为这样会暴露你的密码，一般只加一个 ‐p 但是不给值 
$ mysql ‐u root ‐p 
Enter password: # 这时会要求你输入密码

```

进入 MySQL 客户端的 REPL 环境过后，可以通过标准的 SQL 语句操作数据库。
常见的操作指令：

```mysql
mysql> show databases;  ‐‐ 显示全部数据库 
mysql> create database <db‐name>;  ‐‐ 创建一个指定名称的数据库 
mysql> use <db‐name>;  ‐‐ 使用一个数据库，相当于进入指定的数据库 
mysql> show tables;  ‐‐ 显示当前数据库中有哪些表 
mysql> create table <table‐name> (id int, name varchar(20), age int);  ‐‐ 创建一个指定名称的数据 表，并添加 3 个列 
mysql> desc <table‐name>;  ‐‐ 查看指定表结构 
mysql> source ./path/to/sql‐file.sql  ‐‐ 执行本地 SQL 文件中的 SQL 语句 mysql> drop table <table‐name>;  ‐‐ 删除一个指定名称的数据表 
mysql> drop database <db‐name>;  ‐‐ 删除一个指定名称的数据库 
mysql> exit|quit;  ‐‐ 退出数据库终端
```

### 可视化工具 

如果需要复杂的操作，推荐 Navicat Premium

> 下载地址：http://www.navicat.com.cn/download/navicat-premium
> 这是一个付费软件，可以免费试用 14 天





