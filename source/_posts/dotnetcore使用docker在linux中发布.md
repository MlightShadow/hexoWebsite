---
title: dotnetcore使用docker在linux中发布
date: 2019-01-16 21:28:03 
categories: 
    - 笔记
 
---

### 关于dotnetcore与docker

使用vs构建dotnetcore项目时确实可以添加docker支持, 但是windows安装docker受到windows版本的限制, 所以我只能在linux中生成docker镜像文件

### swagger的发布

swagger配置xml之后尤其是发布之后要注意能够继续访问到, 否则根本无法访问文档

### dotnetcore版本与docker image版本

由于没有找到合适的dotnet2.0版本的镜像文件, 最后只能升级项目到dotnetcore2.2版本, 并且使用dotnet:2.2.0的docker镜像来运行