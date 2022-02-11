---
title: Android 打包应用
top: false
cover: false
toc: true
mathjax: true
tags:
  - Android
categories:
  - 打包
abbrlink: 396a7f69
date: 2021-01-06 16:32:38
password:
summary:
---

官方教程 https://reactnative.dev/docs/signed-apk-android/

Android要求所有应用都必须先使用证书进行数字签名，然后才能安装。 为了通过Google Play商店分发您的Android应用，需要使用发布密钥对其进行签名，然后再将其用于以后的所有更新。 自2017年以来，借助Google Play的应用签名功能，Google Play可以自动管理签名发布。 但是，在将应用程序二进制文件上传到Google Play之前，需要使用上传密钥对其进行签名。 Android Developers文档上的[“签署应用程序”](https://developer.android.com/tools/publishing/app-signing.html)页面详细描述了该主题。 本指南简要介绍了该过程，并列出了打包JavaScript捆绑包所需的步骤。

## 1. 生成上传需要的秘钥

> Android要求所有应用都有一个数字签名才会被允许安装在用户手机上，Android开发者官网上的如何给你的 [应用签名文档](https://developer.android.com/tools/publishing/app-signing.html) 描述了签名的细节  

生成签名有两种方式：

- Keytool命令行
- Android Studio界面生成

您可以使用keytool生成专用签名密钥。 在Windows上，必须从 `C:\Program Files\Java\jdkx.x.x_x\bin` 运行keytool。

>（一定要记得你在那个路径生成的，后面需要用）

```shell
keytool -genkeypair -v -keystore hu-yi-key.keystore -alias huyi-key-alias -keyalg RSA -keysize 2048 -validity 10000

```

⚠️  生成打包用的 key，将 `keystore` 命名为 `hu-yi-key.keystore` 别名 `-alias` 为 `huyi-key-alias` 
 
⚠️  记住要输入的 `输入密钥库口令:`

```shell
# 老命令
keytool -genkey -v -keystore hu-yi-key.keystore -alias huyi-key-alias -keyalg RSA -keysize 2048 -validity 10000
# 官方新命令
keytool -genkeypair -v -keystore hu-yi-key.keystore -alias huyi-key-alias -keyalg RSA -keysize 2048 -validity 10000
# 输入密钥库口令: huyi2021
# 再次输入新口令: huyi2021
# 您的名字与姓氏是什么?
#   [Unknown]:  huyi
# 您的组织单位名称是什么?
#   [Unknown]:  huyi
# 您的组织名称是什么?
#   [Unknown]:  huyi
# 您所在的城市或区域名称是什么?
#   [Unknown]:  shanghai
# 您所在的省/市/自治区名称是什么?
#   [Unknown]:  shanghai
# 该单位的双字母国家/地区代码是什么?
#   [Unknown]:  zh
# CN=huyi, OU=huyi, O=huyi, L=shanghai, ST=shanghai, C=zh是否正确?
#   [否]:  y
#
# 正在为以下对象生成 2,048 位RSA密钥对和自签名证书 (SHA256withRSA) (有效期为 10,000 天): 
#    CN=huyi, OU=huyi, O=huyi, L=shanghai, ST=shanghai, C=zh
# 输入 <huyi-key-alias> 的密钥口令
#   (如果和密钥库口令相同, 按回车):
# [正在存储 hu-yi-key.keystore]
#
# 这是一个巨坑 不要迁移标准格式，否则打包错误

# Warning:
# JKS 密钥库使用专用格式。建议使用 "keytool -importkeystore -srckeystore hu-yi-key.keystore -destkeystore hu-yi-key.keystore -deststoretype pkcs12" 迁移到行业标准格式 PKCS12。
```

⚠️⚠️⚠️ 下面这是一个巨坑 不要迁移标准格式，否则打包错误，上面生成命令会提示下面命令，如果你照做了，坑可能爬不出来

```shell
# Warning:
# JKS 密钥库使用专用格式。建议使用 "
keytool -importkeystore -srckeystore hu-yi-key.keystore -destkeystore hu-yi-key.keystore -deststoretype pkcs12
# " 迁移到行业标准格式 PKCS12。
```

![Android打包](https://gitee.com/hy0916/PictureBed/raw/master/20210106164646.png)

## 2. 设置Gradle变量

![Android打包](https://gitee.com/hy0916/PictureBed/raw/master/20210106165559.png)

如果 Gradle 加载失败，https://gradle.org/ 点击下面按钮重新同步

![Android打包](https://gitee.com/hy0916/PictureBed/raw/master/20210106165742.png)

Android Studio 打包

![Android打包](https://gitee.com/hy0916/PictureBed/raw/master/20210106170348.png)

![Android打包](https://gitee.com/hy0916/PictureBed/raw/master/20210106170456.png)

`Key store path` 是选择你刚才命令行生成的key,根据你存放的路径选择key就行  
`Key store password` 是你设置的 密钥库口令: huyi2021  
`Key alias` 别名是直接刚才生成的，点击那个小图标直接选择就行
![Android打包](https://gitee.com/hy0916/PictureBed/raw/master/20210106170653.png)

![Android打包](https://gitee.com/hy0916/PictureBed/raw/master/20210106171623.png)

安静的等待中。。。
不妨再出一个ios打包？？
![Android打包](https://gitee.com/hy0916/PictureBed/raw/master/20210106171942.png)

ok 顺利完成，我们去找到这个`.apk`的安装包 
![Android打包](https://gitee.com/hy0916/PictureBed/raw/master/20210106172307.png)

根据图片的路径来找，然后直接发送到手机上就可以在手机上安装啦
![Android打包](https://gitee.com/hy0916/PictureBed/raw/master/20210106172535.png)

Android 打包应用到此结束，不妨点下文章下面的小手手吧！！