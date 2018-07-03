---
title: 统计词频Python
date: 2018-06-04 20:30:15
tags:
---
很久没有这个博客了，今天刚好有人问我一个关于英文句子，词频统计的代码该怎么写，我用Python进行了功能实现

代码如下

``` Python
import re


def fenci(string):
    data = re.split(" |,|\.|\?|!", string) 
    return data


def deal_data(data):
    for word in data:
        if word:
            if word in cp:
                cp[word] = cp[word]+1
            else:
                cp[word] = 1


def main():
    string = input('请输入一个英文句子:\n')
    data = fenci(string)
    deal_data(data)
    # 匿名函数处理键值对 返回列表类型
    data = sorted(cp.items(),key = lambda x:x[1],reverse = True)
    print('统计词频如下')
    # 查看数据类型
    # print(type(data))
    for word in data:
        print(word[0], ':', word[1])
    # 上面处理排序 就改变了类型，所以不用下面的字典处理方式
    # for key, value in data.items():
    #     print(key, ':', value)


if __name__ == '__main__':
    cp = {}
    main()
    input('按下任意键继续...')
```