---
title: 关于IP伪造那点事
date: 2017-11-16 14:12:34
tags:
 - 信息安全
---

## 什么是IP伪造

IP伪造就是用一个虚拟的IP，去访问或者连接某台服务器（电脑，主机等终端）。 

## 为什么会有IP伪造？

比如你去投票，显示一个IP只能投票一次，你去登录后台，显示一个IP只能尝试5次，利用IP伪造 我们可以无限制投票，无限制尝试登录。 

## 如何实现？

IP伪造可以通过 HTTP头。

常见字段有

X-Forwarded-For
Client-IP
x-remote-IP
x-originating-IP
x-remote-addr

我用上面第一条写了一段演示代码.
不得不说，Python是真的好用。下面那个居中是因为我不会把他用字符形式输出，它自己以HTML标签显示了emmm

```python
import requests
# 这是 IP138 网站提供的查询地址
url = 'http://2017.ip138.com/ic.asp'
# 这里我们构造IP伪造头
head = {'X-forwarded-for':'49.49.49.49'}
# 访问
r = requests.get(url, headers=head)
r.encoding = ‘GBK’
print(r.text)
<center>您的IP是：[49.49.49.49] 来自：泰国</center>
```

