---
title: Linux&Windows双系统时间错误
date: 2018-12-31 12:36:21
tags:
 - Linux
---

# 闲聊
我其实一直使用Windows操作系统的， 直到上了大学开始，接触的东西慢慢的偏向了Linux操作系统，但是毕竟本人属于网瘾少年，离不开游戏，而虚拟机的话有很多Linux的优势会发挥不出来（个人感觉，尤其是网络通讯方面）。所以最终还是选择了双系统，安装了Windows 10+Ubuntu 18.04。

# 正文
## 0x00 三种时钟
### 实时时钟（REAL-TIME CLOCK, RTC）
实时时钟是PC主板上的晶振及相关电路组成的时钟电路的生成脉冲，它控制着计算机系统的时间。操作系统中所提到的RTC，指的就是在计算机主板控制下的时间，即系统时间，为计算机硬件的内部时钟。
<!-- more -->
### 协调世界时（COORDINATED UNIVERSAL TIME, UTC）
协调世界时（英语：Coordinated Universal Time，法语：Temps Universel Coordonné，简称UTC）是最主要的世界时间标准，其以原子时秒长为基础，在时刻上尽量接近于格林尼治标准时间。

UTC也是计算机系统中的一个时间衡量标准，Ubuntu默认就将机器时间视为UTC。

### 格林尼治标准时间（Greenwich Mean Time, GMT）
格林尼治平时（英语：Greenwich Mean Time，GMT）是指位于英国伦敦郊区的皇家格林尼治天文台当地的平太阳时，因为本初子午线被定义为通过那里的经线。

## 0x01 时差产生的原因
Windows系统认为，BIOS时间就是RTC，不加以修改。
Linux系统认为，BIOS时间是UTC时间。
中国处于东八区（UTC+8），所以导致会产生8小时的误差。
## 0x02 解决方案
解决的办法有下面两种：
1.修改Windows系统为UTC时间，在命令行中输入下面的命令即可。
``` bat
reg add HKLMSYSTEMCurrentControlSetControlTimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1
```

2.修改Ubuntu系统为RTC时间，在命令行中输入下面的命令即可。
``` bash
sudo timedatectl set-local-rtc 1
```