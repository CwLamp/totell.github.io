---
title: 在Ubuntu中配置LAMP环境
date: 2017-06-07 11:20:16
tags:
 -Ubuntu
 -PHP
 -MySQL
 -Apache2
---

## Apache

```bash
# 安装apache服务
apt install apache2
# 启动apache服务
service apache2 start
# 重启apache服务
service apache2 restart
# 停止apache服务
service apache2 stop
```

## MySQL

```bash
# 安装mysql服务
apt install mysql-server
# 启动服务
service mysql start
# 停止服务
service mysql stop
# 重启服务
service mysql restart
```

## PHP

```bash
# 安装PHP
apt install php7.0
# 安装mysql扩展
apt install php7.0-mysql
# 配置Apache
apt install libapache2-mod-php7.0
```

#### 说明

systemd 是一个很好的工具去管理系统服务

