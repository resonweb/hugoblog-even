---
layout: "post"
title: "git小结"
author: "ResonHou"
categories: ["Computer"]
tags: ["GitHub","SoftWare",]
date: 2018-04-04
---
Git作为版本控制工具，有利于多人合作及个人代码的管理。配合使用开放源代码的GitHub远程仓库，可事半功倍！

<!--more-->

# Git常用命令
Git可以安装在Linux及windows系统，这里就不多说怎么安装了。
## 1. 仓库初始化
Git仓库在用户的角度来看，就是一个特定的目录。将一个目录初始化为Git仓库，有两种途径：
### 1.1 无中生有  
一个项目的初始，可以使用这种方法，从0开始写起。  
在系统中新建一个目录（例 ~/sample/ ，也可以是已经存在的目录 ），进入其中。反正确定现在所在的位置（可用pwd命令查看）是你想要创建Git仓库的位置就行了。然后运行命令：  
```
git init
```
这个命令会创建一个隐藏目录 ~/sample/.git/ ，这标志着当前目录已经是一个Git仓库了。
### 1.2 克隆（站在已有的肩膀上）
从一个已经有基础的仓库（一般为远程仓库）克隆一份到本地。命令如下：
```
git clone https://github.com/username/repository.git
```
该命令会在本地主机生成一个目录，与远程主机的仓库同名。如果要指定不同的本地目录名，可以将目录名作为git clone命令的第二个参数:
```
git clone https://.../xxx.git <dirname>
```

## 2. 日常使用
```bash
git branch -a           # 查看所有分支
git checkout -b name    # 新建分支
git status              # 查看git状态
git add -A              # 缓存所有新更改
git commit -m "xx"      # 提交更改到本地仓库，"xx"为备注
git pull <remote repo>  # 拉取远程仓库并合并到本地
git push origin master:gh-pages
                        # 推送本地master分支到origin仓库的gh-pages分支
git remote -v           # 查看远程仓库地址
git remote add <name> http://xxx/xxx.git
                        # 添加远程仓库
```

## 附上师兄写的邮件一封
注：不是写给我看的

你上传到gitlab上的东西我看到了，这个不是git的主流做法。这样传的话我还要重新添加。

git的作用是多个人同时维护一个软件，非常有效。鉴于以后咱们有可能还要经常一起写程序，使用git能大大提高效率。

我把git的主流做法给你说一下，就以添加一个实验为例：

1、下载

2、输入git branch -a可以看得到有哪些分支

3、新建一个分支 git checkout -b name 。

刚下载下来是在master分支上。一般来讲，master分支是存放稳定能用的版本的，不管什么时候从master上下载下来的程序是可以用的，就是为了避免程序改了一半，不能用。

新建一个分支，这个分支上的内容和master是一样的，修改这个分支上的东西不会影响master分支。

4、修改程序

5、git add 将修改放入暂存区

6、git commit -m 提交文件

7、git push 上传到远端

这个时候别人就能看到你的修改内容了。但要注意是修改的内容在你新建的分支上。


4-7步骤不需要是完全修改好之后做，可以在任何时候做，主要是记录每一步做什么，万一后面做错了，方便回滚。

如果完全修改好了，确定没有问题，切换到master分支上（git checkout master），然后把新的分支合并到master上(git merger 新分支名称)，然后再push到远端。最后可以把这个分支删掉(git branch -d name)。


我在这边只需要git pull一下，就能得到跟你电脑上一样的版本。

所以多个人写一个程序的话很方便，不用把整个程序或修改的文件发来发去，写的时候也不用考虑备份的事情，想看改了什么地方也很容易。


不用担心会把软件改坏，git可以回滚的。

这边还有人用git来共同写论文，这样不用把论文源文件传来传去。大家可以同时写，也能看到别人该了哪些地方，也不用把源文件发来发去了。
