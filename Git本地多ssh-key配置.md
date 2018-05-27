# Git本地多个SSH-KEY配置

* 配置环境：Windows10_x64

## ssh-key创建

```cmd
# 跳转到`.ssh`目录下，如果不存在可以手动创建
# 切换到C:\Users\user\.ssh
$ cd ~/.ssh
# 新建工作的SSH key
$ ssh-keygen -t rsa -C "your@email.com"
# 设置名称为keyname..,默认为`id_rsa`
Enter file in which to save the key (/c/Users/user/.ssh/id_rsa): keyname..
```

## 新密钥添加到ssh agent中

```cmd
#因为默认只读取id_rsa，为了让SSH识别新的私钥，需将其添加到SSH agent中
$ ssh-add ~/.ssh/keyname..
#如果出现Could not open a connection to your authentication agent的错误，就试着用以下命令：
$ ssh-agent bash
$ ssh-add ~/.ssh/keyname..
```

## 修改config文件

```cmd
#在~/.ssh目录下找到config文件，如果没有就创建
# code 为配置git默认编辑工具，也可以使用vim
$ code config  # vim config
```

修改后`config`配置如下：

```cmd
# 配置github.com
Host github
HostName github.com
User git
IdentityFile C:/Users/administere/.ssh/id_rsa

# 配置coding.net -1
Host shzhe
HostName git.coding.net
User git
IdentityFile C:/Users/administere/.ssh/id_rsa

# 配置coding.net -2
Host vshzhe
HostName git.coding.net
User git
IdentityFile C:/Users/administere/.ssh/vshzhe_rsa
```

其规则就是：从上至下读取`config`的内容，在每个Host下寻找对应的私钥。这里将GitHub SSH仓库地址中的git@github.com替换成新建的Host别名如：github2，
那么原地址是：git@github.com:funpeng/Mywork.git，替换后应该是：github2:funpeng/Mywork.git.

> 打开新生成的`~/.ssh/id_rsa2.pub`文件，将里面的内容添加到GitHub后台。

## 测试是否配置成功

```cmd
administere@DESKTOP-TOLN0V0 MINGW64 ~/Desktop
$ ssh -T shzhe
The authenticity of host 'git.coding.net (180.97.181.69)' can't be established.
RSA key fingerprint is SHA256:jok3FH7q5LJ6qvE7iPNehBgXRw51ErE77S0Dn+Vg/Ik.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'git.coding.net,180.97.181.69' (RSA) to the list of known hosts.
Hello shzhe! You've connected to Coding.net via SSH successfully!

administere@DESKTOP-TOLN0V0 MINGW64 ~/Desktop
$ ssh -T github
The authenticity of host 'github.com (192.30.253.112)' can't be established.
RSA key fingerprint is SHA256:nThbg6kXUpJWGl7E1IGOCspRomTxdCARLviKw6E5SY8.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'github.com,192.30.253.112' (RSA) to the list of known hosts.
Hi maz0401! You've successfully authenticated, but GitHub does not provide shell access.

administere@DESKTOP-TOLN0V0 MINGW64 ~/.ssh
$ ssh -T vshzhe
Hello vshzhe! You've connected to Coding.net via SSH successfully!
```

## 验证配置

```cmd
administere@DESKTOP-TOLN0V0 MINGW64 /f/GitRepo
$ git clone github:maz0401/study.git
Cloning into 'study'...
Warning: Permanently added the RSA host key for IP address '192.30.253.113' to the list of known hosts.
remote: Counting objects: 155, done.
remote: Total 155 (delta 0), reused 0 (Receiving objects:  75% (1delta 017/), pack-reused 155), 116.01 K154
Receiving objects: 100% (155/155), 133.55 KiB | 13.00 KiB/s, done.
Resolving deltas: 100% (53/53), done.
Checking connectivity... done.

administere@DESKTOP-TOLN0V0 MINGW64 /f/GitRepo/study (master)
$ git remote add coding shzhe:shzhe/study.git
```