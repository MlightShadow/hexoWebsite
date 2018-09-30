---
title: CMaNGOS编译部署教程
date: 2018-08-17 13:27:21
tags: 
    - cmangos
    - wow
categories:
    - 游戏

---
本篇环境为windows  
这个[cmangos](https://github.com/cmangos/mangos-classic "")是他们官网托管在github上的源码库, 官网之前(2018-05)我访问已经没有了, [官网](https://cmangos.net/ "")这个链接我也给出

### 文档
cmangos给出了比较详细的文档, 当然实际操作中会遇到一些问题, 这就是我接下来要介绍的的坑  

现在(2018-09)[文档](https://github.com/cmangos/issues/wiki "")已经移到cmangos的issues中的wiki下了, [Installation-Instructions](https://github.com/cmangos/issues/wiki/Installation-Instructions "")就是包含有我们编译所需要的所有步骤, 我这里不做逐步的演示和翻译

### 环境部署
官网给出了相关windows环境下的下载名单, 首先我编译的时候(2017-11)的源码已经不再支持msvc14以下的版本所以在boost官网上你只能下载 msvc14 和msvc14.1的源码版本, 这点在这里不注意还是会有点麻烦

### 编译
编译这部分完全按照文档给出步骤去操作, 使用CMAKE和vs2015及以上生成就可以了

### DB导入
网上说是需要mysql5.5, 不知道是历史版本的文档还是野狐禅, 当时(2017-11)我使用的是mysql5.7, 但是导入的时候经常会报错, 我这边分拆成小段执行就解决了这个问题,  另外直接远程执行命令会出现问题, 所以后来直接远程到服务器把sql文件直接拷贝过去执行, 再有就是字符的问题, windows这边出现问题注意把文件转成ANSI就好, linux我这边情况不清楚 

### 提取工具
最后编译提取工具CMAKE勾选extractor和game就可以了, 这个地方注意看官网的文档, 执行提取的时候注意执行生成的脚本文件(.sh), 不然提取会有问题