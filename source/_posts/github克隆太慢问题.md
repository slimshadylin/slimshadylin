---
title: github克隆太慢问题
top: false
cover: false
toc: true
mathjax: false
date: 2020-11-30 21:06:27
password:
summary:
tags:
  - github
categories:
  - 环境搭建
---

## 思路

git clone 特别慢是因为 github.global.ssl.fastly.net 域名被限制了。
只要找到这个域名对应的 ip 地址，然后在 hosts 文件中加上 ip–>域名的映射，刷新 DNS 缓存便可。

## 执行步骤

1. 打开网址<https://github.com.ipaddress.com/>，分别搜索

   ```bash
   github.global.ssl.fastly.net
   github.com
   ```

2. 得到 ip

   ![github.com](domain.png)

3. 写入 hosts

   ![hosts](hosts.png)

   ```bash
   199.232.69.194  github.global-ssl.fastly.net
   140.82.114.4  github.com
   ```

4. 刷新缓存
   打开 cmd，执行如下命令

   ```cmd
   ipconfig /flushdns
   ```
