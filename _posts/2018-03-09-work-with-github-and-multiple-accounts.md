---
layout: post
title: 多个github账号提交问题
date: 2018-03-09 15:32:24.000000000 +09:00
tag: other
---

此方法是基于ssh方式的,https方式还没有尝试成功

#### 创建ssh key

`ssh-keygen -t rsa -C "your-email-address"`

将文件保存为id_rsa_COMPANY的格式,并保存到`~/.ssh/id_rsa_COMPANY`

#### 把新的key加入到github上

访问github,https://github.com/settings/keys,创建一个new ssh key,将id_rsa_COMPANY.pub的内容复制上去.

返回终端,输入`ssh-add ~/.ssh/id_rsa_COMPANY`

#### 创建一个配置文件

```javascript
touch ~/.ssh/config
vim config
```

输入

```shell
#Default GitHub
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa

Host github-COMPANY
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_COMPANY
```

#### 修改仓库地址

```shell
git remote set-url origin git@github-COMPANY:Company/testing.git
```

这样就会通过github-COMPANY来找到config文件中对应的仓库

### ref

https://code.tutsplus.com/tutorials/quick-tip-how-to-work-with-github-and-multiple-accounts--net-22574