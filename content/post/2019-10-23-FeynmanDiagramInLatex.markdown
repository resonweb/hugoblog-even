---
layout: "post"
title: "在Latex中画费曼图"
categories: ["学术软件教程"]
tags: ["Latex","FeynmanDiagram",]
date: 2019-10-23
---

目前已经知道了两种可以直接在Latex中画费曼图的方式，  
- \usepackage{axodraw2}，  
- \usepackage[compat=1.1.0]{tikz-feynman}。  

我用的是texlive2019。

<!--more-->
---
### axodraw2
使用这个包有两种方式画费曼图，通常我们会另外安装它的可视化软件`JaxoDraw`，生成eps文件，然后再导入Latex中，但是这样还要再安一个软件，特别是有时候我们没有办法使用`JaxoDraw`。这个时候就可以直接在Latex中输入代码，来生成费曼图。

它使用精确定位的方式来一条线一条线地画费曼图，每一个点都要给出(x,y)坐标。
{{< admonition note "注意事项：" false >}}
   {{< admonition >}}
      - 我使用的环境是`TexLive2019+TexStudio`  
   {{< /admonition >}}
   {{< admonition >}}
      - 编译带有`axodraw2`费曼图代码的文档时，需要按照标准的`dvi-ps-pdf`流程。
   {{< /admonition >}}
   {{< admonition >}}
      - 如果使用`pdfLatex,xeLatex,LuaLatex`，需要使用`axohelp`作为中间步骤，下面详细说明。
   {{< /admonition >}}
{{< /admonition >}}

下面的名词区分参看[我之前的博文]({{< ref "post/2019-09-30-TexIDE.markdown" >}})    
{{< admonition type="note" title="点击打开详细说明" details="true" >}}
   {{< admonition >}}
      所谓的标准`dvi-ps-pdf`流程，也许有些人并不清楚(我也不清楚)，我说明(硬摆和)一下:   
   {{< /admonition >}}
   {{< admonition >}}
      在最初的Tex/LaTex设计中，输出文件其实是dvi文档。为什么不用了呢，大概就是对非英语语言的不友好吧(其实也还在用)。现在最通用的文档格式，我想PDF应该算是第一位了吧，其实还有一种是PS文档，在Arxiv上也是支持的。所以我们现在想要得到PDF文档，怎么办呢？那就转格式，所以就有了`dvips`,`dvipdf`,`ps2pdf`这样的转格式命令。
   {{< /admonition >}}
   {{< admonition >}}
      后来呢，人们嫌这样太麻烦，所以又发明出了`pdfLatex`这样的编译器，它直接编译出来就是PDF文件了。嗯，这下我们比较舒服了，但是这个时候还是有问题（什么问题我也不知道，大概是和字体以及编译速度有关的）。所以就有了后面的`xeLatex,LuaLatex`。我个人的使用上来说，感觉`xeLatex`比`LuaLatex`快一点。所以我现在主要使用`xeLatex`来编译Tex文档。
   {{< /admonition >}}
{{< /admonition >}}
{{< admonition warning "注意" >}}
      使用`xeLatex,LuaLatex`来编译的Tex文档，**必须**是*UTF-8*编码的文档。
{{< /admonition >}}
回到费曼图上来，
1. 为什么不能用好用的编译器来编译axoDraw2的费曼图呢？  
我摘录了一段官方文档：The program here is dvipdf and not the similarly named dvipdfm or dvipdfmx, which are incompatible with axodraw. The reason why dvipdf works is that it internally makes a postscript file and then converts it to pdf.  
意思就是所它使用了一些PS文档的功能，所以PS文档做为中间过程必须要使用。  
2. 用`pdfLatex,xeLatex,LuaLatex`怎么编译axoDraw2的费曼图呢？  
   先用编译器编译一遍，生成一个.ax1结尾的辅助文档，然后使用`axohelp`命令生成.ax2结尾的辅助文档，再用编译器编译一遍。如果你用的命令行，那就是：
   ```bash
   > xelatex    main.tex
   > axohelp    main
   > xelatex    main.tex
   ```
   如果你用的是TexStudio,那可以在设置里自己添加一个编译的方式。步骤是：Options - Configure TexStudio - Build - User Commands, 在这里自己添加一个命令，如  
   `txs:///xelatex | axohelp % | txs:///xelatex`。
3. 哦，还有费曼图的画法啊？  
参看[官方文档](http://mirrors.cqu.edu.cn/CTAN/graphics/axodraw2/axodraw2-man.pdf)吧，有很多例子。

### Tikz-Feynman
首先Tikz本身就是在Latex中画图的工具，Tikz-Feynman是在Tikz基础上，专为画费曼图设计的。  

它可以自动分配第个点的位置。自动分配位置的算法需要`LuaLatex`的支持，所以只能使用`LuaLatex`来编译。看起来智能了一点儿了，画简单图时很方便，但是在画复杂图时，逻辑有点难以理解，我不喜欢。  

同样，使用方法参看[官方文档](https://mirror.bjtu.edu.cn/ctan/graphics/pgf/contrib/tikz-feynman/tikz-feynman.pdf)。

