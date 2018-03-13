---
layout: post
title: centos7上挂载ntfs格式的u盘
date: 2018-03-13 10:32:24.000000000 +08:00
tag: other
---

```shell
#安装epel库
yum --enablerepo=extras install epel-release
#安装依赖包
yum --enablerepo epel install ntfs-3g
#挂载
mount -t ntfs-3g /dev/sdb1 /mnt/usb
```