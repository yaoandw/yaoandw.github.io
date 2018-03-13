---
layout: post
title: 直接在文件系统中将文件加入owncloud
date: 2018-03-13 10:32:24.000000000 +08:00
tag: other
---

```shell
#到occ命令目录
cd /home/wwwroot/default/owncloud
#www是用户
sudo -u www php occ files:scan --all
```
更多命令可以参考

<https://doc.owncloud.org/server/9.0/admin_manual/configuration_server/occ_command.html#file-operations-label>