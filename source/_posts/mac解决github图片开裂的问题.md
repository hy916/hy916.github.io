---
title: mac解决github图片开裂的问题
top: false
cover: false
toc: true
mathjax: true
tags:
  - github
categories:
  - 工具
abbrlink: ceadf6b5
date: 2021-01-05 09:55:20
password:
summary:
---

### 原因分析

国内之所以加载不了github图片，源自于一个叫做“DNS投毒”的问题。简单地说，就是当浏览器向DNS服务器询问域名对应IP时，DNS服务器返回了一个错误的IP地址。很多居心叵测的人会通过DNS投毒污染DNS服务器，将数据引入到他们特定的IP来获取不正当利益。

>如果你对该风险不感兴趣，请跳过直接看下文解决办法。

如果你有在百度上搜索过其它的解决办法，大概他们都会告诉你修改本地hosts就可以了。这个方法确实有效，因为你本地配置hosts之后浏览器就不会再向DNS服务器询问域名的IP，而是以你配置的为准。

但是该方法存在一个明显的问题，很多时候我们配置了网络上别人给的hosts之后确实能够加载图片，但是过不多久他又失效了。而且网络上很多帖子给的IP地址还都不一样。

对于绝大多数人来说是没有能力甄别到底哪个IP是真实的IP地址，如果你随便使用别人提供的IP地址的话，会存在和DNS投毒一样的风险。你的数据很可能被传到了一个私人服务器。

### 解决方案1

通过问题分析，我们知道了是国内DNS服务器被污染导致github图片无法加载。那么解决方案就很明确了，我们只需要使用google的DNS服务器8.8.8.8; 8.8.4.4就可以完美规避这个问题。具体操作如下：

![tu](https://gitee.com/hy0916/PictureBed/raw/master/20210128153655.png)

![tu](https://gitee.com/hy0916/PictureBed/raw/master/20210128153734.png)

### 解决方案2

### 1. mac 用户可以使用SwitchHosts 进行hosts管理  [官网下载](https://oldj.github.io/SwitchHosts/#cn)

![tu](https://gitee.com/hy0916/PictureBed/raw/master/20210105100704.png)

### 2. 开启backup

![开启backup](https://gitee.com/hy0916/PictureBed/raw/master/20210105095945.png)

### 3. 将以下代码复制进去

```
# GitHub Start 
140.82.112.4       github.com
199.232.69.194     github.global.ssl.fastly.net
185.199.108.153    assets-cdn.github.com
185.199.109.153    assets-cdn.github.com
185.199.110.153    assets-cdn.github.com
185.199.111.153    assets-cdn.github.com
199.232.96.133     raw.githubusercontent.com
199.232.96.133     gist.githubusercontent.com
199.232.96.133     cloud.githubusercontent.com
199.232.96.133     camo.githubusercontent.com
199.232.96.133     avatars0.githubusercontent.com
199.232.96.133     avatars1.githubusercontent.com
199.232.96.133     avatars2.githubusercontent.com
199.232.96.133     avatars3.githubusercontent.com
199.232.96.133     avatars4.githubusercontent.com
199.232.96.133     avatars5.githubusercontent.com
199.232.96.133     avatars6.githubusercontent.com
199.232.96.133     avatars7.githubusercontent.com
199.232.96.133     avatars8.githubusercontent.com
# GitHub End
```

### 4. 如果还是不行，那就从这里 [查询ip](https://www.ipaddress.com/) 上查询一下上面的域名对应的ip是否已经改变

![tu](https://gitee.com/hy0916/PictureBed/raw/master/20210105100543.png)
