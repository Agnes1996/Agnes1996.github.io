---
title: "「Python」Demo Code 1"
subtitle: "Python Foundations - Get Web data by requests"
layout: post
author: "Liumt"
header-style: text
hidden: true
tags:
  - Python (爬虫基础)
  - 笔记
---

> 目标：获取淘宝搜索页面的信息，提取其中的商品名称和价格
> 理解： 淘宝的搜索接口 翻页的处理
> 技术路线：requests‐re


------------------

### Demo Code

```
import requests
import re
```

```
def getHTMLText(url):
    headers = {
        'User-Agent':
        'Mozilla/5.0 (Windows NT 6.1; WOW64; rv:23.0) Gecko/20100101 Firefox/23.0'
    }  # 浏览器伪装
    try:
        coo = 't=85db5e7cb0133f23f29f98c7d6955615; cna=3uklFEhvXUoCAd9H6ovaVLTG; isg=BM3NGT0Oqmp6Mg4qfcGPnvDY3-pNqzF2joji8w9SGWTYBu241_taTS6UdFrF3Rk0; miid=983575671563913813; thw=cn; um=535523100CBE37C36EEFF761CFAC96BC4CD04CD48E6631C3112393F438E181DF6B34171FDA66B2C2CD43AD3E795C914C34A100CE538767508DAD6914FD9E61CE; _cc_=W5iHLLyFfA%3D%3D; tg=0; enc=oRI1V9aX5p%2BnPbULesXvnR%2BUwIh9CHIuErw0qljnmbKe0Ecu1Gxwa4C4%2FzONeGVH9StU4Isw64KTx9EHQEhI2g%3D%3D; hng=CN%7Czh-CN%7CCNY%7C156; mt=ci=0_0; hibext_instdsigdipv2=1; JSESSIONID=EC33B48CDDBA7F11577AA9FEB44F0DF3'
        cookies = {}
        for line in coo.split(';'): 
            name, value = line.strip().split('=', 1)
            cookies[name] = value
        r = requests.get(url, cookies=cookies, headers=headers, timeout=30)
        r.raise_for_status()
        r.encoding = r.apparent_encoding
        return r.text
    except:
        return ""
```
注意：

1 需要伪装成浏览器，否则会被拒绝爬取数据。

2 需要使用 try-except结构，使得爬取出现错误时不会中断而是继续运行设计的内容

```
def parsePage(ilt, html):
    try:
        plt = re.findall(r'\"view_price\"\:\"[\d\.]*\"', html)
        tlt = re.findall(r'\"raw_title\"\:\".*?\"', html)
        for i in range(len(plt)):
            price = eval(plt[i].split(':')[1]) # 除去view_price外部引号
            title = eval(tlt[i].split(':')[1])
            ilt.append([price, title])
    except:
        print("")
	
```
^这里用到了正则表达式，可以参考菜鸟教程https://www.runoob.com/regexp/regexp-syntax.html

```
def printGoodsList(ilt):
    tplt = "{:4}\t{:8}\t{:16}"
    print(tplt.format("序号", "价格", "名称"))
    count = 0
    for g in ilt:
        count = count + 1
        print(tplt.format(count, g[0], g[1]))

```
```
def main():
    goods = "休闲游戏"
    depth = 2
    start_url = 'https://s.taobao.com/search?q=' + goods
    infoList = []
    for i in range(depth):
        try:
            url = start_url + '&s=' + str(44 * i)
            html = getHTMLText(url)
            parsePage(infoList, html)
        except:
            continue
    printGoodsList(infoList)


main()
```
在这段实例中，爬取的代码只占一小部分，更多的代码是在清洗整理数据，对Python基础代码能力有一定的要求。数据分析在学习Python的过程中要重视基础语法，不能只盯着数据分析的库。另外在写代码前，要多思考，尽量想到意外的情况，不要一边写，一边调试修改。
