---
layout: "post"
title: "GitCommandPro"
author: "ResonHou"
categories: ["Computer"]
tags: ["GitHub",]
date: 2018-10-20
---

Git命令分为底层命令 (Plumbing) 和高层命令 (Porcelain)，  
本文主要是看底层命令时的笔记，用来了解Git的内部工作机制。  
**常用的Git命令请查看：[Git 小结]({{< ref "post/2018-04-04-GitCommand.markdown" >}})**
<!--more-->
## Git Command Pro.
Git 是一套内容寻址文件系统（content-addressable）。 

|     |     |
| :------------ |:-------------:|
| {{< figure src="/assets/images/Git-1.png"  width="200" >}} | {{< figure src="/assets/images/Git-2.png" width="200" >}}  |

```bash
git init
git hash-object                     # 底层命令，用于存储内容
git cat-file [-p 输出对象内容] [-t 输出对象类型]
git cat-file -p master^{tree}       # 专用：输出master这个commit对象所指的tree对象
git commit-tree SHA -p parentSHA    # 作一次commit，SHA 指提交的tree对象，-p 用来指定父级commit对象
git update-ref refs/heads/test SHA  # 新建或更新一个分支到SHA这个commit对象
git symbolic-ref HEAD [refs/heads/test] # 查看或更改HEAD的引用内容
git update-ref refs/tags/v0.0 SHA   # 新建一个简单标签（lightweight tag）
git tag -a v1.0 SHA -m "comments"   # 新建一个带注释的标签(annotated tag) ，
# 区别在于：lightweight只是一个引用到commit对象的指针; 而annotated是一个tag对象，有自己的SHA值。

git remote add name url     # 添加一个远程仓库，name是你为远程仓库取的别称，url是远程仓库的地址。
                            # `Remote 引用 ` 和 `分支` 主要区别在于他们是不能被 check out 的。
git push origin :topic      # 删除远程的topic分支

git gc      # garbage collect, 将松散对象打包，新commit的对象(blob, tree, commit)成单个文件存储，
            # 打包后成一个文件。
            # 区别在于：打包后只存储最新版的文件，之前的版本将只记录差异。
git verify-pack -v .git/objects/pack/*.idx  # 检查并显示打包过的对象

git log --pretty=oneline    # 显示git日志
```

## file mode:
   * 040000: 文件夹
   * 100644: 普通文件
   * 100664: 普通文件（群组可写）
   * 100755: 可执行文件
   * 120000: 符号链接
   * 160000: Git链接（Gitlink）

## 链接学习

> [参考博客: https://www.howtoing.com/controlling-urls-and-links-in-jekyll/](https://www.howtoing.com/controlling-urls-and-links-in-jekyll/)    

里面有动态链接到自己之前写的博文的方法
