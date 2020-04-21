---
title: "LinuxFilesystemHierarchy"
categories: ["Computer"]
tags: "Linux"
tags: []
date: 2019-10-23
draft: true
---

原文：http://www.tldp.org/LDP/Linux-Filesystem-Hierarchy/html/Linux-Filesystem-Hierarchy.html#Foreward  
Version 0.65  
Binh Nguyen

<!-- more -->

- superblock: 包含文件系统（硬盘或分区）的整体信息
- directory: 包含文件名+inode序号
    - File Name:
    - inode: 除了文件名之外与文件相关的所有其它信息
        - N data blocks: 储存数据的块序号
    - indirect block: inode中可存储的data block数量有限，
    可用indirect指针指向更多的data blocks。

同UNIX一样, Linux 选择单个层级目录结构. 所有的东西都是从根目录出发, 然后展开到相应的子目录中去, 而不是Windows所采用的驱动器(盘符). 在Windows中, 你可以将文件存放在任何一个地方, C/D/E or F盘中, 这样的一个文件系统也是层级结构, 但是却由软件自我管理, 而不是操作系统统一管理. (想一下Windows是不是每一个程序有一个目录,这个目录中的子目录由这个程序自由设定, 而这在Linux下是完全不同的) 另一方面, Linux将某个目录安排得与根目录的远近程度, 取决于这个目录在系统启动过程的重要性.

如果你问为什么Linux使用斜杠/而不是像Windows一样使用反斜杠\, 那仅仅是因为它延续了UNIX的传统. 同时,它也延续了UNIX的区分大小写, this 和 THIS 具有完全不同的意思, 这也就意味着字符的大小写在类UNIX操作系统中非常重要. 新手所遇到的大部分问题可能都是区分大小写这个特性造成的, 特别是不管从可移动磁盘还是通过FTP的文件传输操作中.

在Linux的文件系统中, 文件的存放位置由文件的功能决定, 而不是由它在某个程序中的地位决定. 在这种文件系统中, 由操作系统来统一决定某个应用程序应该将它的文件存放在什么地方.

在Windows中安装一个应用程序, 通常它会将大部分文件存放自己的目录中. 例如帮助文档在Windows中可能在下面三个目录中的其中一个:
- C:\Program Files\[program name]\ 
- C:\Program Files\[program-name]\help 
- C:\Program Files\[program -name]\humpty\dumpty\doo  

而在Linux中, 所有程序都会将帮助文档根据其目的存放在下面这些目录中的一个, 它们都与系统的目录层级保持一致.
- /usr/share/doc/[program-name] For 文档
- /usr/share/man/man[1-9]       For 手册
- /usr/share/info               For 信息

所有的Linux用户都知道, 除非