# 生物信息高性能集群  

## 一、操作说明    

**说明：`$`后为命令，其他的为输出或说明。**  

终端  
Windows:Text terminal推荐[putty](https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe), Xterm推荐使用[MobaXterm](https://mobaxterm.mobatek.net/download.html)  
Mac or Linux: `ssh -Y username@serverip`  

```
登录服务器10.100.128.160
`ssh -l username 10.100.128.160` (公共用户public，密码public123)  

对于计算量较大的任务，请不要在登录节点上直接运行，以交互式方式qrsh登录到计算节点，或者用qsub提交任务
```
### Linux基本操作  

**掌握以下常用的Linux命令：**

|  |  |  |  |  |   |   
|  --- | --- | --- | --- | --- | ---  |
|  ls | cd | mv | rm | pwd | top  |
|  ps | grep | kill | file | tar | cat  |
|  less | more | chmod | chown | vim (vi) | time  |
|  cp | scp | ln | mkdir | wget | git  |
|  find | export | source | mount | head | tail  |

**使用集群**  
尽量不要在登录节点（管理节点）上运行大型程序，集群已部署好SGE作业调度系统  
**（一）交互式方式登录**  
登录管理结点后，请用`qrsh`以交互式方式登录计算节点，系统会自动分配并登录到计算节点。一般普通的小的计算任务采取交互式方式登录  
**（二）用qsub递交任务脚本**  
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

**Linux学习资料**  
[Linux command line](https://github.com/hnnd/Linux_command_line)

**生物信息学非常有用的一行代码集成**  
      [Bioinformatics one-liners](https://github.com/hnnd/oneliners)
