---
layout: "post"
title: "MadGraph5_aMC教程"
author: "ResonHou"
categories: ["学术软件教程"]
tags: ["SoftWare",]
date: 2018-05-05
---
理论物理高能唯象学的分析流程是一个繁锁的过程，但大体上分为理论的程序化、从理论中预言可观测量、数据分析并与实验数据对比。  
本文主要立足从理论中预言可观测量部分，解说计算工具包：MadGraph5_aMC
<!--more-->
## 安装  
### 环境要求
- Ubuntu 系统（或者其他Linux发行版）
- 可连网
- 最好有界面（主要用于使用浏览器下载安装包）  

### 下载安装  
> 资源下载：[MadGraph5_aMC@NLO](https://launchpad.net/mg5amcnlo) in Launchpad.  
> 点击页面右侧的绿色版本下载安装包（ ubuntu默认下载到目录：~/Downloads/ ）  

然后运行下面的命令:  

```bash
cd ~/Downloads                  # 进入下载的压缩包所在的目录
tar -xzvf MG5_aMC_v***.tar.gz   # 解压 "***"代表版本号
cd ./MG5_aMC_v***               # 进入 MG5 所在的目录
./bin/mg5_aMC                   # 运行 MG5 ，命令行提示符变为：MG5_aMC>
```

### 使用 Pythia 和 Delphes
MadGraph5_aMC 可实现除计算散射截面、产生事例之外更多的功能，通过使用内置的下载脚本下载插件实现。可下载用于实现**强子化**的工具 Pythia ，用于实现快速探测器模拟的工具 Delphes 或者 PGS ， 用于事例分析的工具 MadAnalysis 等。
```bash
MG5_aMC>install pythia8         # MG5_aMC>只是提示符，代表 MG5 开启，不用输到命令行，其后面的才是命令
MG5_aMC>install Delphes         # 注意区分大小写，在输入 install 后，可点击两次 Tab 键，显示所有的选项。
```
其他的选项可自行查阅[ MG5 说明书](https://arxiv.org/abs/1405.0301v2)。

{{< admonition type="note" title="TroubleShooting" >}}
在MG5_2.7.3版本中，直接调用上面安装 Delphes 的方式，会出现编译错误的情况。</br>
解决方式就是选择手动编译安装，命令见下面代码块。
{{< /admonition >}}
```bash
# 下载源码，两种方式二选一
wget http://cp3.irmp.ucl.ac.be/downloads/Delphes-3.4.2.tar.gz && tar -zxf Delphes-3.4.2.tar.gz
git clone https://github.com/delphes/delphes.git    # 备用方式

cd Delphes-3.4.2                # 进入源码目录
mkdir build && cd build         # 新建并进入 build 目录

# 构建任务信息，并指定安装位置（用实际 MG5 的目录替换 ‘/PATH/TO/MG5’）
cmake -DCMAKE_INSTALL_PREFIX=/PATH/TO/MG5/Delphes '..'

# 编译并安装 Delphes, -j 后的数字是调用的内核数量
make -j8 install                
```


## 使用说明
> **此文章全篇默认当前目录为** `MG5_aMC_vxxx/`

MadGraph5_aMC 可用于实现指定模型下的任意过程计算，最终给出过程的散射截面，并且产生用于后期分析的事例文件。  
### 初级操作

#### 产生代码并运算代码
> 技巧：单击 `Tab` 键补全命令，双击 `Tab` 键显示所有可选项  

```bash
MG5_aMC>import model sm         # 导入模型文件
MG5_aMC>generate p p > t t~     # 产生pp到tt的过程（仅为举例），语法参考 MG5 说明书附录
MG5_aMC>display diagrams        # 显示过程费曼图
MG5_aMC>output ./process/pptt   # 生成代码，存储在当前目录下的 ./process/pptt/ 目录中
MG5_aMC>launch                  # 运行代码，计算过程的截面，且产生事例
```
launch 命令可以不运行，只是生成代码，不运算。当要运算时，先进入代码目录（例：./process/pptt/），再执行 `generate_events` 命令开始计算。这种方式等价于直接运行 `launch` 命令，不同之处在于这样可以多次运算代码，产生多个事例文件。
```bash
cd ~/Downloads/MG5_aMC_***/process/pptt/    # 以实际路径为准
./bin/generate_events           # 开始计算
```
#### 运算代码前的设置（很重要）
> 强调：这部分很重要，可详细阅读界面内容。

当开始运算代码的之后，会出现如下图的交互界面：  
![jiaohu.png](https://i.loli.net/2018/05/05/5aedc3746933d.png)  
这是让你设置是否使用 Pythia 和 Delphes 的，若使用 Pythia ，可以输入 1 ，点击`Enter`键。可以详细阅读这部分内容，根据需要设置好之后，输入 0 ,点击`Enter`键。  
之后会出现一个类似的界面，用于编辑参数卡片。输入 1 ，可编辑 param_card.dat 文件。

所有卡片文件都存放在代码目录的 ./process/pptt/Cards/ 目录中，可以在运算代码之前更改相关卡片文件。

### 高级操作
这部分主要是想要说明使用 proc_card.dat 文件，来将上面的命令集成到一个批处理文件中。并没有什么高级的命令。  
刚解压的 MG5 根目录中存在一个 proc_card.dat 文件例子，可以参照着将所有命令写在这个文件中，然后运行 MG5 时带上文件参数。
```bash
./bin/mg5_aMC proc_card.dat
```

## MG5_aMC 目录结构及意义
鉴于现在的程序学习过程操作大于意义的实际情况，我将详细的物理意义放在操作之后进行说明。  
### 目录结构

.  
├── bin  
├── Delphes  
├── HEPTools  
├── input  
├── INSTALL  
├── madgraph  
├── models  
├── process  
├── pythia-pgs  
├── README  
└── VERSION  

| 一级目录 | 内容说明 |
|:-|:----|
| ./ | 代表 MG5根目录 |
| ./bin/ | 目录中存在两个可执行脚本，其中 `mg5` 是一个过时的脚本，其代码指向另一个脚本 `mg5_aMC` 。也就是说两个脚本等价，保留前一个脚本只是为了兼容之前的版本，并给出一行过时提醒。`mg5_aMC` 脚本只是 MG5 程序包的入口，作用是检查一下环境设置，然后调用 `./madgraph/` 目录中的主程序。 |  
| ./Delphes/   | 目录只有在 `install Delphes` 之后才会出现。插件程序包将逐渐移至 `HEPTools/` 目录中。|
|  ./HEPTools/ | 目录存放着通过 `install` 命令安装的相关程序包及 `install` 命令本身。如果想更改默认的插件下载地址，可更改 `./HEPTools/HEPToolsInstallers/` 目录中的相应 python 脚本。|
| ./input/ | 目录中存放着 MG5 的初始化参数，如 multiparticles 设置等。重点是 `./input/mg5_configurations.txt` 文件中设置了 MG5 的关联程序包路径。|
| ./madgraph/ | MG5 主程序 |
| ./models/ | 模型包文件 |
| ./process/ | 手动添加的目录，用于存储具体计算过程代码 |
| ./README ./INSTALL | 说明性文件，分别介绍用法和安装过程 |



**事例目录中子目录的说明：**  
./ &nbsp;&nbsp;&nbsp;&nbsp; 指代事例目录，如：`process/pptt`  
├── bin &nbsp;&nbsp;&nbsp;&nbsp; 存放可执行文件  
├── Cards &nbsp;&nbsp;&nbsp;&nbsp; 存放卡片文件，可以运算代码之前修改  
├── Events &nbsp;&nbsp;&nbsp;&nbsp; 存放事例文件  
│   ├── run_01 &nbsp;&nbsp;&nbsp;&nbsp; 每产生一次事例，则产生一个run_0x目录  
│   └── run_02 &nbsp;&nbsp;&nbsp;&nbsp; 存放着 HEP 和 root 格式事例文件  
├── HTML &nbsp;&nbsp;&nbsp;&nbsp;  HTML格式的报告  
└── index.html &nbsp;&nbsp;&nbsp;&nbsp; 报告首页，可用浏览器打开  

### 工作流程的意义
1. `import model` 命令从 ./models/ 目录中导入一个具体的模型，如标准模型为 `import model sm`  

2. `generate` 是产生一个具体的物理过程，学过费曼图的人应该都知道什么是物理过程的。如经典的正负电子到正负缪子的过程可写为 `generate e+ e- > mu+ mu-`。  

3. `display diagrams` 用来查看过程的费曼图，通常是被省略的。

4. `output ./process/` 用来将代码导出到指定的目录，以便重复使用。  
以上命令只是用来写出具体计算的代码。因为脚本语言运算的速度太慢，所以只是用脚本语言帮我们去写一个针对特定过程的 C++ 语言代码（即所谓的硬代码）。这种流程在任何事例产生器程序中都通用，FeynArts 是写成了 Fortran 代码，CalcHEP 也是写成了 C++ 代码。  
对应到物理意义中，以上代码中已经将振幅写好，并已经取了 **模平方** 。执行代码只是用来作相空间积分，但是积分的过程又不能解析计算，所以只能采用 Monte Carlo 模拟的方式。这种方式就需要产生事例，用来模拟出来积分截面。

5. `launch` 命令是 MG5 中附带的一个脚本，用来执行 `./process/XXXX/bin/generate_events` 命令。  
这一步是开始执行以上代码，不过在做相空间积分，计算出数值结果之前，需要指定模型参数、对撞参数等，如粒子质量、对撞能量、PDF。这些参数分为存放在两个主要的卡片文件中：`param_card.dat` 和 `run_card.dat` 中。
