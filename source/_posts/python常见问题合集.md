---
title: python常见问题合集
top: false
cover: false
toc: true
mathjax: false
date: 2020-08-17 23:51:55
password:
summary: 整理工作学习中python的常见问题
tags:
  - python
categories:
  - 编程
---

# anaconda

以下多个问题操作，均没有配置 anaconda 为系统环境变量

## 多个虚拟环境安装

如果系统中已经安装了 python，但是不同的开发环境对 python 的版本和第三库的版本要求不同，这个时候就可以通过 anaconda 安装多个虚拟环境解决

## pip 安装第三方库

anaconda 中安装第三方库怎么操作呢？
进入 anaconda 的安装目录，进入`/Scripts`目录，然后执行 pip 命令即可成功安装

> pip install xxx

## pip 升级

进入 anaconda 根目录，也就是 python.exe 的目录

> python -m pip install --uprade pip

或者在 pip.exe 所在目录

> pip install pip -U

## 配置第三方镜像源

以下的一次性生效的配置，不用修改配置文件，windows 和 linux 都直接通过 cli 解决，本人比较喜欢的阿里源

> pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/
> pip config set install.trusted-host mirrors.aliyun.com

清华源

> https://pypi.tuna.tsinghua.edu.cn/simple

还有个临时的方法

> pip install xxx -i https://pypi.tuna.tsinghua.edu.cn/simple
