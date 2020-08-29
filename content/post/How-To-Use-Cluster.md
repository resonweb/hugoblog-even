---
title: "How to Use Cluster"
date: 2020-05-01T17:07:25+08:00
lastmod: 2020-05-01T17:07:25+08:00
draft: false
tags: []
categories: []

reward: false
mathjax: false
mathjaxEnableSingleDollar: false
mathjaxEnableAutoNumber: false
---
关于怎样使用学院服务器集群的说明。
<!--more-->

## 校外使用VPN服务
First, You need connect to the campus network through VPN service.

In this step, you'd better use the "[EasyConnect](https://vpn.ccnu.edu.cn/com/installClient_en.html)" Application, and use your CCNU campus account.

By the way, the "Server Address" needed by the EasyConnect is "vpn.ccnu.edu.cn".

## 登录学院集群
Second, You need connect to the computer cluster through SSH service.  

In this step, your just need to open a terminal if you use GNU/Linux or MacOS.
If Windows, you'd better use "[PuTTY](http://www.putty.be/latest.html)" or XShell for convenience.  

Then type and execute the following command:  
`ssh -p 1362 usr_02@202.114.36.19`

If you did the above steps right and the network is fine, after this command,
you will get a message letting you input a password, and that is the password I told you.


## 集群使用
### 文件传输
小的脚本，可以直接在远程服务器上编写，远程编辑器有 **vim** 和 **nano** 供你选择。  
但总还是有些时候必需在**本地**和**服务器**之前进行文件传输。  
方法有：  
1. 图形化工具  
- GNU/Linux下有：[gftp](https://www.gftp.org/)
- Windows: [xftp]()属于xshell套装，收费。
- MacOS: I do not know.
2. 命令行工具  
在本地终端运行命令：
`sftp -P 1362 usr_02@202.114.36.19`

sftp登录完成以后，可以使用ls | cd | get | put 四个命令来完成上传与下载。
ls and cd 我就不再说了。
```bash
get file.txt            # 下载文件
put file.txt            # 上传文件
```

### 正式提交任务
Furthermore, when you login the remote server, that is to say you have input the
password and got a prompt, like "usr_02@admin ~$". Then you can use the server
as you own PC.

但是，集群有集群的使用规则，你必须将你的程序交给集群的 **自动管理软件slurm** 来帮你
执行。方法是将你的命令写在一个脚本中，*我已经有写好的脚本模板，放在本文最后*。  

你只需要更改脚本中的一行数据，即可通过以下命令提交任务了:  
`sbatch run.slurm`

在run.slurm中，需要修改的地方就是在“开始执行我们的任务”下面加上你要运行的命令，
文件中有例子，形如：
`srun math -script yourScript.wl`

### 简单调试
{{< admonition >}}
此方法仅用于调试，切勿跑大型任务。</br>
This method is used for debuging. Do not submit a large task.
{{< /admonition >}}

Third, How to use Mathematica at the cluster?

This is a sophisticated problem. I have installed the mathematica under this
server account. And you can run it through the following command:  
`math -script yourScript.wl`

##  Troubleshooting

Possible problem:  The VPN service is not stable, it will disconnect to the campus network

at any time, you can restart the EasyConnect APP to fix this problem.

## run.slurm

```bash
#!/bin/bash

#---------------------- 申请资源 ----------------------#
#-- 以 "#SBATCH" 开头的为 Slurm 专用参数,#号后不能有空格 ---#

#SBATCH --job-name=Job_1            ### 指定作业名称
#SBATCH --partition=middle          ### 指定作业运行的分区
                                    ### low | middle | high | batch
# #SBATCH --nodelist=comput18       ### 指定作业运行的节点,可不指定,由系统分配

#SBATCH --nodes=1                   ### 使用节点数量
#SBATCH --ntasks=2                  ### 总任务数,总进程数
#SBATCH --ntasks-per-node=2         ### 每个节点上的任务数量,大于任务数/节点数,不要超过 56
#SBATCH --cpus-per-task=2           ### 单任务使用的CPU核心数
### SBATCH --mincpus=               ### 每个节点上最小的线程数(逻辑CPU数)

#SBATCH --output=%j.txt             ### 本来输出到屏幕的内容写入文件中, %j 代表作业ID
#SBATCH --error=%j_error.txt        ### 本来输出到屏幕的错误信息写入文件中
#SBATCH --qos=ztyu_qos              ### 设置任务优先级
                                    ### 可用 sacctmgr show qos 查看

#--------------------- 打印开始信息 ---------------------#
### 打印作业分配的资源信息, 这些信息写在output文件中
### 包括作业名称, ID, 分配的节点, 当前时间
printf " Job Name: $SLURM_JOB_NAME "  
printf " Job ID: $SLURM_JOBID "       
printf " Allocate Nodes: $SLURM_JOB_NODELIST\n"
printf "任务开始时间: "
date

#------------------ 开始执行我们的任务 ------------------#

# echo "我只打印一次"                    ### 测试打印一次
# srun echo "我在 $HOSTNAME 上执行了!"   ### 测试打印, 次数由任务数决定
# srun math -script yourScript.wl       ### 运行mathematica程序, 后面脚本的名字自行修改
#                                       ### 上面都是注释
srun math -script yourScript.wl

#--------------------- 打印结束信息 ---------------------#
printf " Job Name: $SLURM_JOB_NAME "  
printf " Job ID: $SLURM_JOBID "       
printf " Allocate Nodes: $SLURM_JOB_NODELIST\n"
printf "任务结束时间: "
date
```