# Git客户端安装-Windows

[Git下载地址：https://github.com/git-for-windows/git/releases](https://github.com/git-for-windows/git/releases)

下载`Git-2.17.0-64-bit.exe`版本,进行安装。安装方式运行以后，直接默认下一步即可。

## #生成ssh-key

```cmd
$ ssh-keygen -t rsa -C "yourmail@xx.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/c/Users/vshzh/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /c/Users/vshzh/.ssh/id_rsa.
Your public key has been saved in /c/Users/vshzh/.ssh/id_rsa.pub.
The key fingerprint is:
SHA256:XQrrHnwy9fsKi0jhj55WLDZYYi0cEw85kRjptX3sGiM yourmail@xx.com
The key's randomart image is:
+---[RSA 2048]----+
|  .++=           |
|  o Bo           |
| . o B...   .    |
|  . * + o+ o     |
|   . =.+S +      |
|    E.*++. .     |
|     ooB* o .    |
|     .o* * o .   |
|     o= + . oo.  |
+----[SHA256]-----+

$ ls
id_rsa  id_rsa.pub
```

## #克隆远程仓库：

现在，可以通过git clone命令克隆远程仓库了，在各自的电脑上运行：

```cmd
$ git clone git@192.168.2.130:/home/git/gitrep/sample.git
Cloning into 'sample'...
warning: You appear to have cloned an empty repository.

#如果ssh默认端口不是22，如770，在克隆时，需要加上端口号
$ git clone git@192.168.2.130:770/home/git/gitrep/sample.git
```