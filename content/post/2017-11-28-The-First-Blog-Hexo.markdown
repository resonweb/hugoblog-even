---
layout: "post"
title: "TheFirstBlog--Hexo"
author: "ResonHou"
date: 2017-11-28 09:47:32
categories: ["Computer"]
tags: ["Hexo","Blog",]
date: 2017-11-28
---

欢迎来到侯镖锋的[个人博客](https://reson-hou.github.io/blog/),此博客于2017年11月28日正式开通.

本来我只是手写了一个小一点的[个人主页](https://resonweb.github.io),但是后来无意中发现了这个可以批量生产静态博客页面的工具[Hexo](https://hexo.io)!捯饬了好几天后,终于可以用自己的方式上传,并正式运行了.

在这里大力感谢[GitHub](https://github.com)站点提供的服务支持!

<!--more-->




## 基础
### GitHub
[GitHub](https://github.com)是开源代码的天堂,这里汇聚了各式各样的开源项目,你可以自由的Copy或者提供自己的贡献. 我认识它已经很久了,不过之前只是象征性的玩一下,并不深入. 因为我并没有什么好的东西要在这个地方写,并与大家分享. 虽然我一直想要做一个自己的[个人主页](https://reson-hou.github.io),不过由于内容的不足,只能以一个空壳子的形式放在那里.
后来通过由iissnan写的[ProGit](http://iissnan.com/progit/)学习Git这个版本管理工具,然后就控制不住地去看了一下他的个人主页[Vi](http://iissnan.com).被他主页上的动画效果给吸引到了(注:GitHub只提供静态页面,我一个没有学过JavaScript的人,被惊艳到也是可以理解的). 然后顺滕摸瓜,发现他自己写了一个Hexo的模板[NexT](http://theme-next.iissnan.com), 接着就发现了[Hexo](http://hexo.io).

### Hexo
正如上面说的, Hexo 是一个可以批量生产静态博客页面的工具,是前端开发者为了"懒"而开发的自动渲染页面的傻瓜式软件. 但是学习这个工具的过程也是有曲折的,这正是我这篇博文的主要内容.
Hexo 是基于[Node.js](http://nodejs.cn)(你并不需要知道这是个什么东东)而开发的专门用来做博客站点的开发工具.所以安装Hexo之前,需要先安装 Node.js 以得到基础支持.

### 方案规划
也正是有了前面提到的那个空壳子,才让我的Hexo学习之路多了许多不必要的麻烦. 一是我想要布署一个基于Hexo的博客站点;二是我并不想要放弃之前写的那个粗糙到不能看的半成品(毕竟那是一行一行代码自己敲的啊!!)

我的计划方案是保持原来的[个人主页](https://reson-hou.github.io)不动,在这个站点下面放一个子目录 `./blog/`, 将基于Hexo开发的博客站点放在 blog 下面. 这个动作看其来并不难,但是我却走了不少的弯路,以至中途试过放弃这个方案. 我就不写中间的傻瓜流程了,只写最后的成功流程吧.(也许错误的流程才能学到更多的东西,不过太过于杂乱,我就是这样傲娇地放弃了^_^)

## 安装开发环境
首先说明我的开发环境是 Ubuntu 17.10
并且已经安装过了 Git
安装过程也可以参考 [Hexo Docs](https://hexo.io/zh-cn/docs/index.html)

### Node.js
可以从[ Node.js 官网]下载后解压,然后添加到环境变量中,也可以用下面的方法:
Wget:
```
wget https://raw.github.com/creationix/nvm/master/install.sh | sh
```
注:我的电脑上没有curl, 所以就没有用这个方法.

然后重启终端,运行下面的命令:
```
nvm install stable
```

### Hexo
所有必备的应用程序安装完成后,即可使用 npm 安装 Hexo 了. (npm 是 node.js 的包管理命令)
```
npm install -g hexo-cli
```

## 开始建站
### 初始化工作目录
在任意地方运行下面的命令:
``` bash
hexo init <folder>
cd <folder>
npm install
```
注: `folder` 是你想要将站点放入的本地工作目录,请写出准确的路径(eg: ~/work/hexo)
    以后默认省略 `folder` , 当前工作目录也默认为 `folder`

你可以查看一下 `folder` 目录中的文件, 详细结构请看[https://hexo.io/zh-cn/docs/setup.html](https://hexo.io/zh-cn/docs/setup.html). 不过要注意以下几个文件或目录:

_config.yml : 这个是站点的主参数设置文件;
themes/     : 个性化主题放置的地方;
source/_posts/ : 里面存放着你写的所有稿件,以后写博文也是编辑这里面的文件;

### 下载 NexT 主题
运行下面的命令:
``` bash
cd themes/
git clone https://github.com/iissnan/hexo-theme-next.git
cd ../
```
注:两个 `cd` 命令只是更换工作目录, 中间的那行是从 git 上克隆一个主题到本地.

### 参数配置
主要参数文件为: hexo_site/_config.yml
``` bash
vim _config.yml
```
对其中部分参数加以说明:

| 参数名 | 参数说明 |
|:--|:-----|
| title | 网站标题 |
| subtitle | 网站副标题 |
| description | 网站描述,用于搜索引擎检索 |
| author | 您的名字 |
| language | 网站所使用的语言,由主题提供 |
| timezone | 网站时区(空着就好) |
| url | 您的站点网址(eg: [https://reson-hou.github.io/blog](https://reson-hou.github.io/blog)) |
| root | 网站根目录(eg: /blog/ ) |
| new_post_name | 新文章的文件名称(eg: :year-:month-:day-:title.md) |
| theme | 选用的主题(eg: next) |
| deploy | 发布站点(如使用 GitHub, 可忽略这个,手动发布就好) |

### 服务器 hexo-server
若还没有安装这个模块,可以运行下面的命令安装:
``` bash
npm install hexo-server --save
```
安装完成后,可以用以下命令开启本地服务器:
``` bash
hexo server
```
然后在浏览器地址栏中输入 `localhost:4000/` ,按 `Enter` 就可以看到你的博客了,惊喜不?
或者按着 `Ctrl`, 点击终端内的地址.

## 发布站点
因为我之前有一个空壳子站点,所以发布有别与普通的发布.
若你的 GitHub 站点是新的,或者想要放弃原来的,重新部署,也可以直接使用 `hexo deploy`
使用方法可参看[Hexo Documents](https://hexo.io/zh-cn/docs/deployment.html)!

我的方法:
  1. 克隆原来的站点到本地;
  2. 新建一个分支 "Blog", 在分支中加入 `./blog/` 目录;
  3. 在一个不同于 Git 的 `Hexo_site` 目录中写博客,并用 `hexo generate` 命令产生页面(全部放在 Hexo_site/public/ 目录中);
  4. 用shell脚本完成删除原本的博客,复制新的博客页面,完成衍合, push 到 GitHub 上.

shell 脚本内容如下:
```
#! /bin/bash

cd ~/work/hexo
hexo clean       # 清空之前产生的页面
hexo g           # 产生新的页面
# hexo s	   # 开启本地网页服务器

###################################################
# Used for uploading the generated "public"
# directory to ~/work/git/reson-hou.github.io/blog/
# with a new git branch, named by "Blog"
###################################################

cd ~/work/git/reson-hou.github.io/
git checkout Blog

rm -rf ~/work/git/reson-hou.github.io/blog/*    #为了避免下面的复制产生冲突
cp -r ~/work/hexo/public/* ~/work/git/reson-hou.github.io/blog/
git add blog
git commit       # 这个命令会让你输入提交信息,可使用[-m "new blog"]参数,但不建议使用.
echo "Upload complete!"

###############################################
#  已经上传到本地仓库,下面用于 push 到 GitHub
###############################################
cd ~/work/git/reson-hou.github.io/

# 下面这种做法是将Blog分支与master分支做了衍合
# 但是我并没有直接这么做,因为我想要用Blog分支做测试
# git checkout master
# git merge Blog
# git push origin master

# 下面是我真正的做法,若是在浏览器中测试可以了,再手动衍合
git checkout Blog
git push origin Blog:master

```

More Info : [https://hexo.io/docs](https://hexo.io/zh-cn/docs/index.html)
