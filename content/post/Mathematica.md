---
title: "Mathematica"
date: 2020-04-21T09:37:20+08:00
lastmod: 2020-04-21T09:37:20+08:00
draft: false
keywords: ["Mathematica"]
description: "A little knowledge about mathematica"
tags: ["SoftWare","Mathematica"]
categories: ["学术软件教程"]
---

Mathematica 是一个符号计算领域十分强大的软件，依托于它们自己开发的 Wolfram 语言及方便使用的 NoteBook， 使其在科学计算等众多领域有广泛的使用。   
它的唯一不便之处在于其版权：一不开源，二收费。所以请大家使用盗版时注意，切勿安心理得。

<!--more-->

---
## 使用方式
### NoteBook
这个方式使用起来就不必我赘述了。

### 命令行使用
> 参见：[官方说明](https://reference.wolfram.com/language/ref/program/WolframKernel.html)  

有两种方式可以在命令行中使用mathematica
1. `math -script yourFile.wl`   
math: 等价的命令还有`math`，`wolfram`,`MathKernel`,`WolframKernel`。  
yourFile.wl: 这个文件中的语句就是NoteBook中的语句。可以用NoteBook直接SaveAs成wl格式，但要注意需要先把NoteBook中的Cell转成 ”Code“ style。  
方法：选中Cell; 快捷键`Alt+8`;
2. `./yourFile.wl`  
在文件开头加上 sharp-bang
```bash
#!/home/reson/bin/math -script

Print["Hello World"]
```

## 高圈计算
高能物理的高圈计算可能会使用FeynArts-FormCalc-LoopTools套装，详情请移步[官网](http://www.feynarts.de/)。  

### Installation
在其官网给出了一个自动安装的[脚本](http://www.feynarts.de/FeynInstall)，你可以直接保存到本地想要安装这三个软件的目录，比如 `~/.Mathematica/Applications/` 。这个目录是 mathematica 自动加载的目录，安装到这个地方，后面就不用再修改 mathematica 的初始化路径了。  
具体方法如下：
``` bash
mv FeynInstall ~/.Mathematica/Applications/
cd ~/.Mathematica/Applications/
sh FeynInstall
```
这个脚本会分别询问你是否安装FeynArts-FormCalc-LoopTools这三个软件  
并在最后询问你是否将 FeynArts and FormCalc 添加到Mathematica的初始化路径中  

### Maybe Problems
#### MathLink
这是一个 MatheMatica 提供的方便调用外部程序的库，正在被 WSTP 这个 API 所代替。  
它提供了一个类似gcc的编译程序mcc，用法如 `mcc test.c -o test.exe`。  
这样编译出来的程序就可以在Mathmatica中使用`Install["test"]`来调用了。  

但是，mcc依赖有系统的动态连接库，如果系统老旧，或其它原因，系统动态连接库存在问题，则mcc将无法编译。
针对LoopTools就是在`bin`目录下只有`lt`，而没有`LoopTools`这样一个可执行程序。  

{{< admonition tip "解决方法" >}}
官网提供有编译好的版本，在这个<a href="http://www.feynarts.de/looptools/">页面</a>的下边有一个:</br>
"Ready-made MathLink executables (Version x.xx, statically linked as far as possible)"  </br>
括号中的意思是”尽可能地使用静态连接库“。然后就可以根据不同的平台，下载相应的版本。
{{< admonition example >}}
移动下载的文件到LoopToops的bin目录下</br>
重命名为 LoopTools</br>
chmod 755 LoopTools
{{< /admonition >}}

{{< /admonition >}} 

