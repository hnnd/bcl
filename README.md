# 生物信息高性能集群  

## 一、登录服务器    

**说明：`$`后为命令，其他的为输出或说明。**  

终端  
Windows:Text terminal推荐[putty](https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe), Xterm推荐使用[MobaXterm](https://mobaxterm.mobatek.net/download.html)  
Mac or Linux: `ssh -Y username@serverip`  

```
登录服务器10.100.128.160
`ssh -l username 10.100.128.160` (公共用户public，密码public123)  

对于计算量较大的任务，请不要在登录节点上直接运行，以交互式方式qrsh登录到计算节点，或者用qsub提交任务
```
## 二、Linux基本操作  

**掌握以下常用的Linux命令：**

|  |  |  |  |  |   |   
|  --- | --- | --- | --- | --- | ---  |
|  ls | cd | mv | rm | pwd | top  |
|  ps | grep | kill | file | tar | cat  |
|  less | more | chmod | chown | vim (vi) | time  |
|  cp | scp | ln | mkdir | wget | git  |
|  find | export | source | mount | head | tail  |

## 三、使用集群    
尽量不要在登录节点（管理节点）上运行大型程序，集群已部署好SGE作业调度系统  
**（一）交互式方式登录**  
登录管理结点后，请用`qrsh`以交互式方式登录计算节点，系统会自动分配并登录到计算节点。一般普通的小的计算任务采取交互式方式登录  
```
$ qstat
job-ID  prior   name       user         state submit/start at     queue                          slots ja-task-ID 
-----------------------------------------------------------------------------------------------------------------
    360 0.60500 P4b8da0fc1 wangys       r     11/29/2018 15:12:48 all.q@cu05                         4        
    364 0.60500 Pe5ba00728 wangys       r     11/29/2018 15:12:48 all.q@cu03                         4        
    366 0.60500 P42b37ecd2 wangys       r     11/29/2018 15:12:48 all.q@cu01                         4        
    370 0.60500 Pcf5d430df wangys       r     11/29/2018 15:12:48 all.q@cu05                         4        
    371 0.60500 P31028d02c wangys       r     11/29/2018 15:12:48 all.q@cu01                         4        
    374 0.60500 P3b88ad32c wangys       r     11/29/2018 15:12:48 all.q@cu06                         4        
    375 0.60500 Pdee72dde4 wangys       r     11/29/2018 15:12:48 all.q@cu03                         4        
    377 0.60500 P0c019e107 wangys       r     11/29/2018 15:12:48 all.q@cu01                         4        
    380 0.60500 P63cfc830b wangys       r     11/29/2018 15:12:48 all.q@cu06                         4        
    391 0.60500 P1aaabc6e3 wangys       r     11/29/2018 15:12:48 all.q@cu04                         4        
    392 0.60500 Pea85ae407 wangys       r     11/29/2018 15:12:48 all.q@cu06                         4        
    394 0.50500 QRLOGIN    wangys       r     11/30/2018 09:00:22 all.q@cu02                         1    
```
其中标记为QRLOGIN的便是刚才交互式登录的进程，可以看出系统自动分配到cu02节点上。以交互式方式登录的在你退出登录或关机后资源会被系统收回  

**（二）用qsub递交批量任务**  
较大的计算任务推荐使用SGE作业管理系统提交任务，先将任务脚本存放在一个文件中，然后用`qsub`提交任务，下面是一个简单的任务`work.sh`, 任务的脚本文件work.sh中包含以下内容：  

```
#!/bin/bash
#$ -S /bin/bash
#$ -N JobName
#$ -cwd
#$ -j y
sleep 60
```

用`qsub`提交任务，`qstat`查看任务运行情况  

```
$ qsub work.sh
$ qstat
job-ID  prior   name       user         state submit/start at     queue                          slots ja-task-ID 
-----------------------------------------------------------------------------------------------------------------
    132 0.55500 P36f0869fb wangys       r     11/29/2018 14:52:18 all.q@cu02                         1        
    133 0.55500 JobName    wangys       r     11/29/2018 15:02:33 all.q@cu05                         1        
    134 0.55500 JobName    wangys       r     11/29/2018 15:02:48 all.q@cu01                         1        
    135 0.55500 JobName    wangys       r     11/29/2018 15:02:48 all.q@cu05                         1        
    136 0.55500 JobName    wangys       t     11/29/2018 15:02:48 all.q@cu01                         1        
    137 0.55500 JobName    wangys       r     11/29/2018 15:02:48 all.q@cu02                         1        
    138 0.55500 JobName    wangys       t     11/29/2018 15:02:48 all.q@cu05                         1        
    139 0.55500 JobName    wangys       r     11/29/2018 15:02:48 all.q@cu03                         1  

```

## 四、一些有用的资料  
**Linux学习资料**  
[Linux command line](https://github.com/hnnd/Linux_command_line)

**生物信息学非常有用的一行代码集成**  
      [Bioinformatics one-liners](https://github.com/hnnd/oneliners)
