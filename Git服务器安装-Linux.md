# #Git服务器安装-Linux

## #运行环境

* 服务器：ubuntu-16.04.3 64bit (git version 2.7.4)
* 客户端：windows10 64bit(git version 2.17.0.windows.1)

## #安装步骤

在安装前，将用户切换到`root`下，一下操作均基于root用户。

### #安装Git

```cmd
root@study-virtual-machine:/home# apt-get install git

#安装成功后，使用`git --version`查看安装版本
```

### #创建Git用户

```cmd
root@study-virtual-machine:/home# id git
id: ‘git’: no such user
root@study-virtual-machine:/home# adduser git
root@study-virtual-machine:/home# passwd git
```

### #创建Git仓库

在`/home/git/`下创建仓库，设置`/home/git/sample.git`为仓库。
修改Git仓库拥有者（owner）为git:

```cmd
root@study-virtual-machine:/home/git/gitrep# mkdir sample.git
root@study-virtual-machine:/home/git/gitrep# git init --bare sample.git
Initialized empty Git repository in /home/git/gitrep/sample.git/.git/
root@study-virtual-machine:/home/git/gitrep# chown -R git:git sample.git/
```

### #创建登录证书

在`/home/git/`目录下创建`.ssh/authorized_keys`文件。把客户端公钥导入文件，一行一个公钥。
调整`.ssh`目录权限

```cmd
root@study-virtual-machine:/home/git# chmod 700 .ssh
root@study-virtual-machine:/home/git# cd .ssh
root@study-virtual-machine:/home/git/.ssh# chmod 600 authorized_keys
```

### #禁用shell登录

出于安全考虑，创建的git用户不允许登录shell，这可以通过编辑`/etc/passwd`文件完成。找到类似下面的一行：

```cmd
git:x:1001:1001:,,,:/home/git:/bin/bash
```

**改为：**

```cmd
git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell
```

设置完成后，git用户可以正常通过ssh使用git，但无法登录shell，因为我们为git用户指定的git-shell每次一登录就自动退出。