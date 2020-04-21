---
layout: "post"
title: "Root-MadAnalysis-CheckMATE"
author: "ResonHou"
categories: ["学术软件教程"]
tags: ["SoftWare",]
date: 2019-09-30
---
理论物理高能唯象学的分析流程是一个繁锁的过程，但大体上分为理论的程序化、从理论中预言可观测量、数据分析并与实验数据对比。
本文主要立足于数据分析并与实验数据对比，解说分析工具包：Root, MadAnalysis, and CheckMATE
<!--more-->

高能物理的实验数据，就像是一缸杂乱的豆子，而数据分析就是要根据不同豆子的属性（颜色，大小等）
来将豆子分类，并查数，做统计。  

凭直觉我们也应该知道，这是一个简单的**重复性**劳动，所以我们可以交给计算机做**循环**。
但是在此之前，我们要先交待清楚，豆子有什么属性（如重量），属性取值在什么样的范围(0-20克)，
我们关心的范围在哪里（红色，9-10克，直径小于2cm），而这些对于计算机来说都是**判断**(if语句)。

## 说明
读完上面的话，大概能明白接下来的这三个工具了，但要记住：它们的功能远不止这些。  

### Root
作为全球最大的科学合作组织(CERN)开发出来的产品，绝对的质量保证，全世界人用了都说好。**然而**，  
1. 初学成本太高；
2. 作为Framework，功能太过繁多。  

于是，针对特定的任务，有了下面这两个简易的工具。

不过还是要声明：  
- 如果你有这样的毅力，直接用Root就可以了，其它的什么都是浮云。
- MadAnalysis and CheckMATE 也要调用 Root 来实现其功能，所以照样得安Root。

### Python 版本
由于 python2 已经于2020年1月1日正式停止更新，但是 MadAnalysis5 和 CheckMATE 还没有出 
python3 版本，所以我们可以使用 Anaconda2(python2) 作为临时方案，当然 Anaconda(python3)
也是避免多次安装 python 常用库的非常好的选择。

<!-- ### MadAnalysis5 and CheckMATE -->


## 下载与安装  
### 环境要求
- Ubuntu/Mint/Deepin 系统（非Debian家族发行版命令会有所不同）
- 可连网
- 最好有界面（主要用于使用浏览器下载安装包）  


### 资源链接
- 资源下载：[Root](https://root.cern.ch/downloading-root)， 
[MadAnalysis5](https://launchpad.net/madanalysis5)， 
[CheckMATE](https://checkmate.hepforge.org/online_tutorial/web_ver2/index.php)  
- 根据不同的环境在页面上找到对应的下载链接（ ubuntu默认下载到目录：~/Downloads/ ）  

> 关于安装:
哎，看我博客的有多少人能明白Linux的安装，其实不过就是一个编绎-连接出可执行文件的标准C语言流程。
顶多执行一下文件的移动操作。好吧，这里假装你知道这些东西，不知道你就跟着做就好了。

### 安装Root
这一步是必须的，因为MadAnalysis和CheckMATE都需要Root做支撑。

root程序会依赖一些库或者软件，[点这里](https://root.cern.ch/build-prerequisites#ubuntu)可以查看
Ubuntu系统的依赖包及其安装方法。但是有一些可选择的包由于更新迭代，名字产生了变化，所以建议分成多次安装，以免报错。
```bash
        # 这个黑框里是root所依赖的包
        # 这几条命令易出错，可分解执行，每次少安装两个
> sudo apt-get install git dpkg-dev cmake g++ gcc
> sudo apt-get install binutils libx11-dev libxpm-dev libxft-dev
> sudo apt-get install libxext-dev
        # 以上为必要组件，以下为建议组件。
> sudo apt-get install gfortran libssl-dev libpcre3-dev
> sudo apt-get install libglew-dev libftgl-dev libfftw3-dev
> sudo apt-get install graphviz-dev libavahi-compat-libdnssd-dev
> sudo apt-get install libldap2-dev python-dev libkrb5-dev
> sudo apt-get install libqt4-dev
        # 以下两行第一行是新版本名字，第二行是系统自带不用安也行。
> sudo apt install default-libmysqlclient-dev libcfitsio-dev libgsl1-dev
> sudo apt install libglu1-mesa-dev libxml2-dev
```
```bash
> mkdir ~/programs/root		
        # root不建议安装在源码的目录里，而是建议新建一个用于安装root的新目录
> cd ~/programs/root            
        # 进入这个新建的目录
> cmake -Dminuit2=ON -Dfftw3=OFF ~/root-xxxx		 
        # root-xxxx为你解压的目录，参数是为了安装checkmate作准备。
> cmake --build . -- -j8 		        
        # 注意空格，j后面的数字为CPU核数
	# Have a big cup of coffee, please!
> source ~/programs/root/bin/thisroot.sh
        # 最后这句是为了启用root的环境变量，
        # 可将其写入Shell的初始化脚本中，见下
```
```bash
> echo $SHELL
        # 如果你看到了bash, 执行第二条命令
        # 如果你看到了zsh，执行第三条命令
> vi ~/.bashrc
> vi ~/.zshrc
        # 我假设你会用vi编辑器
        # 在文件的开头加入下面这句话,别带#号
        # source ~/programs/root/bin/thisroot.sh
```

### Root In Manjaro
Root 已经被收录进了 pacman 的 Community 仓库，我们可以直接从仓库中构建。
这样的好处是别人已经帮我们编译过了，省去了我们再次编译的时间（也就是上面写的
**Have a big cup of coffee**的时间）。我们下载下来的已经是编译好的二
进制可执行文件。

如果使用 Pamac 图形安装工具，可以清晰地看到 Root 的依赖库和可选依赖库， 
我选择的有 gcc8-fortran 和 Pythia8 两个可选的依赖库。

当然，我们也可以选择自行编译，但其中的依赖包库我搞不清楚，官方也没有对 ArchLinux
系进行安装说明，所以我选择相信社区的力量。

### 安装 MadAnalysis5
因为这个程序包是python写的，所以不需要编译，直接解压就可以用了。

```bash
        # 你把 ma5 解压到哪里了？
        # 假设在 ~/programs/madanalysis5/
> cd ~/programs/madanalysis5
> ./bin/ma5
        # 好了，你已经开始运行ma5了。
        # 第一次用，它会问你用多少个内核
        # 来跑 ma5，写最大值就行。
> exit  # 退出
```

除了 madanalysis5 本身，它也依赖一些基它的程序包，你可以在
ma5 里面运行`install package-name`来安装它们。

### 安装CheckMATE
参考[官方安装指南](https://checkmate.hepforge.org/tutorial/ver2/start.php)