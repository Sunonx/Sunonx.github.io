# The Use of Shell



## Linus  shell

[一切从菜鸟开始](https://www.runoob.com/linux/linux-shell.html)

### $ sh deploy.sh

**前言**:用shell脚本部署markdown文章托管至github平台

- windows下使用shell脚本需安装[git](https://git-scm.com/downloads)
- 以下为脚本部署内容，deploy.sh  存放在本地站点目录下和public同级，参考[一键备份博客源文件与发布文章到Github和Coding](https://huaien.co/technology/one-click-script-deploy-hugo/)

```
#!/bin/bash
echo "............................"
echo ".开始执行文章发布更新与同步."
echo "............................"
echo "进入博客的public目录 /E:/Pipx Blog/mysite"
hugo -D
echo "进入博客的public目录 /E:/Pipx Blog/mysite/public"
cd public
echo "-----------------开始将public同步到origin---------------------"
git add .
git commit -m "update"
git pull origin master
git push  origin master
echo "同步到origin仓库完成..."
echo "---------------同步public到仓库结束---------"
```

- 脚步思路：将git命令串起来，由脚本一键部署
- 思考：如何同时将BLOG源文件部署到github上，因.git文件内容的限制，还未能正常执行··· 原本想 文章md内容部署后，删去public中.git文件，后创建站点目录的.git，后因.git配置问题，频频出错，故放弃。为防止博客源文件丢失，可隔时手动部署。或参考其他部署方式。
- 脚本完成后，需修改 public下隐藏文件夹 .git中 config 文件 

```
[core]
	repositoryformatversion = 0
	filemode = true
	bare = false
	logallrefupdates = true
	symlinks = false
	ignorecase = true
[remote "origin"]
	url = git@github.com:Sunonx/Sunonx.github.io.git
	fetch = +refs/heads/*:refs/remotes/origin/*

```

- url 换成自己的，前提需配置好 ssh
- 最后使用git 运行deploy.sh 文件  `$ sh deploy.sh`

不要走开，广告之后，马上回来。😝

### 简介

- Shell 是一个用 C 语言编写的程序，它是用户使用 Linux 的桥梁。Shell 既是一种命令语言，又是一种程序设计语言。

- Shell 是指一种应用程序，这个应用程序提供了一个界面，用户通过这个界面访问操作系统内核的服务。

- Ken Thompson 的 sh 是第一种 Unix Shell，Windows Explorer 是一个典型的图形界面 Shell。

发现一个好玩的  [伪shell脚本博客]()    ········？在哪呢·······哈哈，有点忘记它掉在哪里了。



​                                                                    <center>· end ·</center>
