---
layout: "post"
title: "Manjaro新篇"
author: "ResonHou"
categories: ["Computer"]
tags: ["Linux","Manjaro",]
date: 2020-04-07
---

我之前就已经尝试着用过Manjaro，但是由于存在某些误解与思维定式的阻碍，所以放弃了一段时间。  
相中了Mint，又用了Deepin。各有千秋，兜兜转转，我又回来了。  
对于一个喜欢折腾的人来说，这里就是天堂。

<!--more-->

## 下载与安装
下载地址：[https://manjaro.org/download](https://manjaro.org/download/)  
- 由于滚动更新机制，请尽可能下载最新的安装包  
- 官方提供的桌面：Xfce4 / Gnome / KDE  
- 官网社区版桌面推荐： Cinnamon / i3-wm  

我使用的Xfce4桌面，轻量且定制性高。

## 软件安装
### 更改软件源
更新之前，先更改包管理器pacman的源到国内镜像。  
- 方法一：手动更改`/etc/pacman.d/mirrorlist`文件
1. 打开`/etc/pacman.d/mirrorlist`文件  
2. 搜索关键词"China"  
3. 将下面的"Server"参数移动到文件开头  
- 方法二：使用`pamac`图形包管理工具  
1. 打开`pamac`  
2. 在右上角的打到"首选项-官方软件仓库"  
3. 选择下拉列表中的"China"  
4. 同时可以在这里开启AUR(Arch User Repository)，一个软件宝库。以前之所以说Manjaro缺少软件支持，是因为不知道AUR的存在。

另外：以添加archlinuxcn仓库为例，介绍新仓库的添加方法。
1. 打开`/etc/pacman.conf`  
2. 在最后加上：
```
[archlinuxcn]
SigLevel = Optional TrustedOnly
Include = /etc/pacman.d/archlinuxcn
```
3. 创建新文件`/etc/pacman.darchlinuxcn`，内容如下：  
```
Server= https://cdn.repo.archlinuxcn.org/$arch
Server= https://mirrors.zju.edu.cn/archlinuxcn/$arch
Server= https://mirrors.ustc.edu.cn/archlinuxcn/$arch
Server= https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
Server= https://mirror.xtom.com.hk/archlinuxcn/$arch
Server= https://mirrors.hustunique.com/archlinuxcn/$arch
Server= https://mirrors-wan.geekpie.org/archlinuxcn/$arch
Server= http://mirrors.opencas.org/archlinuxcn/$arch
Server= http://mirrors.cnssuestc.org/archlinuxcn/$arch
Server= http://mirrors.163.com/archlinux-cn/$arch  
Server= http://mirrors.cqu.edu.cn/archlinuxcn/$arch
```

### Upgraded
在安装新软件之前，请勿必先更新初始系统。
```bash
sudo pacman -Syu	# If something goes wrong, like "error: failed to commit transaction (conflicting fils)"
			# Then use the following commands
sudo pacman -Qo *** 	# Where * is the error file's absolutly path
sudo pacman -Rc		# Do this, But remind you must know what you are doing.
sudo pacman -Syu    	# Then upgrade you system
```
### 安装基础包
先列出安装命令
```bash
sudo pacman -Qg base-devel
sudo pacman -S base-devel
sudo pacman -S ranger atool hightlight w3m
sudo pacman -S fcitx fcitx-configtool fcitx-qt5
sudo pacman -S code		
sudo pacman -S libreoffice-still libreoffice-still-zh-cn
sudo pacman -S i3 rofi volumeicon variety picom 
sudo pacman -S virtualbox linux54-virtualbox-host-modules
```
在Manjaro中已经预装了zsh和git, 所以不必重复安装。
以上安装也可以使用图形工具 Pamac  
对上面的命令解释一下：
1. "base-devel"是一个组包(package group)，查看一个组包内的具体包列表可以使用"Qg"选项。
2. 安装"base-devel"组包
3. 安装终端文件管理器 ranger，后面三个是它的预览功能所依赖的包。
4. 安装小企鹅输入法，这个在下面单独再说明一下。  
5. 安装vs code，它在Pamac图形包管理器中显示为Code-OSS。   
6. 安装 LibreOffice 套装及其汉化包。
7. 安装图形界面的窗口管理器 i3 [选装]。  
	在i3下开启variety自动更换壁纸，volumeicon托盘音量调节，nm-applet托盘网络设置，
	xfce4-power-manager托盘电量管理，fcitx托盘输入法。  
	在i3下触控板如果出问题了，参看[Blog](https://blog.csdn.net/weixin_30296405/article/details/97998297),
	或者[ArchWiki](https://wiki.archlinux.org/index.php/Touchpad_Synaptics_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87))
8. 安装虚拟机，出问题了参看[Manjaro Wiki](https://wiki.manjaro.org/index.php?title=Virtualbox)


注：小企鹅输入法说明  
1. 安装完 fcitx 后，还需在`~/.xprofile`中加入输入法选项才可以。
```bash
export GTK_IM_MODULE="fcitx"
export QT_IM_MODULE="fcitx"
export XMODIFIERS="@im=fcitx"
```
2. 如果安装时, 是英文安装，则需要先将系统调成中文，重新登录才可以输入中文。  
方法是去`/etc/locale.conf`更改`LANG=zh_CN.utf8`  
然后在终端中运行`sudo locale-gen`  
重启，在lightdm界面右下角修改`en_GB.utf8`为`zh_CN.utf8`  
3. 英文系统下默认不添加拼音和五笔输入法，需要手动添加。尽量使用Fcitx自带的输入法，响应速度快。  
也可以下载使用SogouPinYin，但是五笔输入法的候选框乱码，我也就不再折腾了。
4. 最后一个qt5包是必须的, 不然 texstudio 无法输入中文.

{{< admonition tip "tip" >}}
注：修改默认 Shell 为 zsh 
{{< /admonition >}}
```bash
sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
1. 使用oh-my-zsh作为其模板库，使用别人写好的主题模板。  
oh-my-zsh的仓库在github上，但是github在国内不太好用，所以有人在Gitee上准备了一个[备用仓库](https://gitee.com/mirrors/oh-my-zsh)，上面就是用的Gitee上的地址。  
2. 用 `chsh` 命令更改自己的默认Shell, 新Shell必须是绝对地址`/usr/bin/zsh`  
也可以直接修改`/etc/passwd`文件中最后一行。

### 国内软件及字体
对于QQ和微信，仍然是Deepin-wine的方案。网易云有Linux版的DEB包。这些本来不可在Arch Linux下使用的软件，经过各位大神的手之后，都出现在了AUR中。

使用Pamac安装软件列表如下：
1. netease-cloud-music
2. deepin-wine-qq / deepin-wine-wechat / linuxqq
3. wps-office-cn / foxitreader
4. texstudio / texmaker
5. zotero / JabRef
6. goldendict
6. latern-bin
7. ttf-ubuntu-font-family / ttf-windows / ttf-dejavu-sans-mono-powerline 

注：下载的主题，图标，字体可以直接放入`/usr/share/`目录下对应的 themes , icons , fonts 目录下。

## 其它
### 系统时间
如果刚安装的系统时间不对，可以用下面的命令同步NTP时间，并写入硬件时间，这样重新开机时间就是正确的了。
如果是双系统，Windows 与 linux 的硬件时钟不一致，也会出现时间的问题，同样可以用这个方法修正。
```bash
sudo ntpdate ntp1.aliyun.com
	# 同步NTP时间
sudo hwclock -w
	# 写入硬件时钟
```

### EasyConnect
因为疫情不能回学校，需要使用VPN连接学校内网，所以就要安装EasyConnect。  
AUR中有，但是版本与学校用的不一致，所以需要手动修改PKGBUILD文件，将里面的
source 和 md5sums 两个字段中的DEB包给替换掉。
``` 
source=("http://download.sangfor.com.cn/download/product/sslvpn/pkg/linux_01/EasyConnect_x64.deb"
        "http://ftp.acc.umu.se/pub/GNOME/sources/pango/1.42/pango-1.42.4.tar.xz")
md5sums=('6ed6273f7754454f19835a456ee263e3'
        'deb171a31a3ad76342d5195a1b5bbc7c')
```

<!--
## 生产工具安装
### Install TexStudio
详见：[**点这里，点这里**](https://techknight.eu/2015/09/30/setup-latex-environment-linux-manjaro-pacman/)
```bash
sudo pacman -S texlive-most		# 安装TexLive的常用包
sudo pacman -S texlive-lang		# 非英语支持
sudo pacman -S texstudio		# 安装Tex编辑器（IDE）
```

### Install root(cern)
由于官网给出的平台不包含Manjaro，所以照着Fedora的依赖包安装。库名可能不一样，我用的是zsh，会自动补全，用相近的包名安装了依赖包。
[点这里](https://root.cern.ch/build-prerequisites#opensuse)查看依赖包。
```bash
mkdir ~/programs/root		# root不建议安装在源码的目录里，而是建议新建一个用于安装root的新目录
cd ~/programs/root
cmake ~/root-xxxx		# 假设你解压源码到了root-xxxx目录
cmake --build . -- -j8 		# 注意空格，j后面的数字为CPU核数
				# Have a big cup of coffee, please!
source ~/programs/root/bin/thisroot.sh
```

### Install MG5
MadGraph5_aMC的具体细节请移步到[MadGraph 教程]({{ site.baseurl }}/{% post_url 2018-05-05-MadGraph5_aMC %})

下载解压后，用MG5(2.6.4)自带的脚本安装LHAPDF6出问题，所以自己手动解决安装。  
- 去LHAPDF的[官网下载](https://lhapdf.hepforge.org/install.html)  
- 解压后，用标准的configure-make来安装   
- 最后记得在.zshrc中添加环境变量，PATH, PYTHONPATH, LD_LIBRARY_PATH
- 修改 `MG5/input/mg5_configuration.txt` , （可以不修改，已经在环境变量里了）

### Install Delphes
由于在Manjaro系统中关于rpc库的文件换了路径（/usr/include/tirpc/rpc），所以会导致Delphes编译出错。解决方法是在Delphes的Makefile中修改两行，加入库的索引。参看：[https://cp3.irmp.ucl.ac.be/projects/delphes/ticket/374](https://cp3.irmp.ucl.ac.be/projects/delphes/ticket/374)

具体操作为先运行 `./configure`，然后修改Makefile中的下面两行：  
> CXXFLAGS += *** -I/usr/include/tirpc		# 中间的星号代表原有的东西不变，空一格加上tirpc的路径  
> DELPHES_LIBS = *** -Itirpc     

最后再运行 `make -j4`

### Install CheckMATE
由于Manjaro系统默认使用python3，而CheckMATE使用的是python2，所以得修改默认的python版本。方法是在用户家目录下建一个`bin`目录，并把它加到系统变量$PATH的前面。之后用下面两条命令在这个bin目录下建立两个快捷方式。
```bash
ln -s /usr/bin/python2.7 $HOME/bin/python
ln -s /usr/bin/python2.7-config $HOME/bin/python-config
sudo pacman -S python2-pip
```
最后，在解压过的CheckMATE目录中，使用`./configure`, `make -j4`就可以编译了。 
-->
