---
title: git绑定多账号和多平台
top: false
cover: false
toc: true
mathjax: false
date: 2022-11-22 17:24:57
summary:
tags:
- git
categories:
- git
---

# git绑定多账号和多平台

## 生成ssh密钥

1. 执行命令,生成多个密钥,xxx为自己的邮箱账号,执行完后会在~/.ssh文件夹下生成对应的密钥,其中以pub结尾的公钥需要在github或者gitlab配置

> ssh-keygen -t rsa -C "xxx@xxx.com" -f ~/.ssh/id_rsa_1

> ssh-keygen -t rsa -C "xxx2@xxx.com" -f ~/.ssh/id_rsa_2

2. 添加密钥到高速缓存中，有几个执行几次

> ssh-add ~/.ssh/id_rsa_1

> ssh-add ~/.ssh/id_rsa_2

3. 查看添加结果

> ssh-add -l

4. 编辑~/.ssh/config文件

``` sh

Host host1
  HostName github.com
  User user1
  IdentityFile ~/.ssh/id_rsa_1

Host host2
  HostName github.com
  User user2
  IdentityFile ~/.ssh/id_rsa_2

```

5. 测试连通性

> ssh -T git@host1

> ssh -T git@host2

如果出现如下打印代表配置没有问题

``` sh

xxx@xxx .ssh % ssh -T git@host1
Hi xxx! You've successfully authenticated, but GitHub does not provide shell access.

```
