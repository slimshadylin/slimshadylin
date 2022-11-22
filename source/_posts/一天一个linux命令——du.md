---
title: 一天一个linux命令——du
top: false
cover: false
toc: true
mathjax: true
date: 2020-11-15 14:44:30
password:
summary: du命令详解
tags:
- linux
- 磁盘
categories:
- linux
---

# du命令详解

# 常用命令

# 查看文件夹大小
``` bash
[xxx ~]$ du -h -d 1
1.8G	./xxx
4.0K	./.xxx
16K	./.xxx
0	./.xxx
32M	./xxx
0	./.xxx
440M	./xxx
307M	./xxx
4.0K	./.xxx
2.5G	.

```

# 查看文件夹所属分区
``` bash
[xxx data1]$ df /home
Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/sda5       xxx         xxx  xxx       10%  /
```

# 查看文件系统分区情况
``` bash
[xxx data1]$ df -lh
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda5       xxxG  xxxG  xxxG  xxx% /
devtmpfs        xxxG     0  xxxG   0% /dev
tmpfs           xxxG     0  xxxG   0% /dev/shm
tmpfs           xxxG  xxxM  xxxG   xxx% /run
tmpfs           xxxG     0  xxxG   0% /sys/fs/cgroup
/dev/sda1       xxxM  xxxM  xxxM  xxx% /boot
/dev/sda2       xxxM  xxxK  xxxM   xxx% /boot/efi
tmpfs           xxxM     0  xxxM   0% /run/user/0
/dev/sdb        xxxG  xxxM  xxxG   xxx% /data1
tmpfs           xxxM     0  xxxM   0% /run/user/1001
```
