---
layout: post
title:  Ubuntu初始化设定
date:   2014-11-12
category: "技术"
---

多服务器管理中格式化是必不可少的。

- 配置用户和组

```
root@AY140519083555626db7Z:~# groupadd admin
root@AY140519083555626db7Z:~# useradd -m -g admin tony
root@AY140519083555626db7Z:~# id tony
uid=1000(tony) gid=1000(admin) groups=1000(admin)
root@AY140519083555626db7Z:~# 
root@AY140519083555626db7Z:~# passwd tony 
Enter new UNIX password: 
Retype new UNIX password: 
passwd: password updated successfully
```
- 改主机名

```
root@AY140519083555626db7Z:~# echo 'CDN' > /etc/hostname
root@AY140519083555626db7Z:~# vim /etc/hosts
root@AY140519083555626db7Z:~# hostname newhostname
```
- 做完自动登录发现自动登录后默认是dash，修改到bash

```
$ echo $SHELL
/bin/sh
$ id
uid=1000(tony) gid=1000(admin) groups=1000(admin)
$ sudo chsh -s /bin/bash tony
[sudo] password for tony: 
```

- vim设置 ~/.vimrc

```
"自动对齐
set autoindent
"行号
set ruler
"高亮当前行
set cursorline
"查找时关键词高亮
set hlsearch
"高亮显示匹配的括号
set showmatch
"缩进
set tabstop=4
set shiftwidth=4
set softtabstop=4
set expandtab
"
set encoding=utf-8
"
syntax on
"记住上次编辑位置
au BufReadPost * if line("'\"") > 0|if line("'\"") <= line("$")|exe("norm '\"")|else|exe "norm $"|endif|endif
```

- bash设置 /etc/bashrc

```
shopt -s checkwinsize
case `id -u` in
    0)
        PS1="`hostname`# "
        ;;
    *)
        PS1="\A \h [\$PWD] -\u- "
        set -o vi
        ;;
esac
```

- 自动登录设置

```
ssh-keygen -t rsa
ssh-copy-id -i ~/.ssh/id_rsa.pub root@IP
```
