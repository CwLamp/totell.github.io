---
title: Pycharm远程Linux开发和调试
date: 2018-01-19 17:31:01
tags: 
 - Python
 - Pycharm
---
## 遇到了点小问题，需要用到这个方法，写下来记录一下，方便以后自己查看

### 先来配置远程Linux主机信息
选择Tools->Deployment->Configuration
在弹出的界面中，点击左上角的 + ，再次弹出的界面中，名字就随便啦，Type选择 SFTP就可以。
确定后在你看到的界面中可以看到关于连接的相关信息，这里填写IP User Password等，就不多说了
在Mappings Item中，选择local path（本地目录）与 Deployment path（远程主机的目录）
完成后，通过Tools->Deployment->Browse Remote Host就可以看到你远程主机的信息
<!-- more -->
### 再来配置远程主机的Python
找到 File->Settings->project:* 然后Add Remote...
新界面中,选择SSH Credentials,填写Linux的服务器信息并选择Python路径
最后保存即可

### 测试部分
可以新建一个hello.py 写完之后记得上传，然后运行就可以查看结果啦
