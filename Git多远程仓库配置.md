# 配置多个远程仓库

以sample项目为例，在Github的地址是git@github.com:git_user/sample.git，在Git@OSC的地址是git@git.oschina.net:osc_user/sample.git。

## 单个远程仓库配置

```cmd
# 添加远程仓库
# git remote add <rep_name> [rep_url]
# rep_name 远程仓库别名，一般默认origin
$ git remote add origin git@github.com:git_user/sample.git
$ git add .
$ git commit -m 'First commit'
$ git push -u origin master
```

## 多个远程仓库配置

通过命令添加多个远程仓库，保证这个“别名（rep_name）”不重复既可。

```cmd
# 配置多个仓库
$ git remote add origin git@github.com:git_user/sample.git
$ git remote add osc git@git.oschina.net:osc_user/sample.git
$ git add .
$ git commit -m 'First commit'
$ git push -u origin master
$ git push -u osc master
```

* 注：`git push -u`中的`-u`参数为第一次提交使用，作用是把本地的`master`分支和远程的`master`分支关联起来，简化命令，之后提交不需要这个参数。

运行几条命令，我们便可以把同一次提交提交到多个远程库，为了方便，我创建了一个`push.sh`的脚本，内容是：

```cnt
#!/bin/bash
echo 'Push to origin master'
git push origin master
echo 'Push to osc master'
git push osc master
```

这样每次提交，我就可以只运行这个脚本就可以，十分方便。