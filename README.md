# 生物信息高性能集群  

## 一、操作说明    

**说明：`$`后为命令，其他的为输出或说明。**  

终端  
Windows:Text terminal推荐[putty](https://the.earth.li/~sgtatham/putty/latest/w64/putty.exe), Xterm推荐使用[MobaXterm](https://mobaxterm.mobatek.net/download.html)  
Mac or Linux: `ssh -Y username@serverip`  

```
登录服务器10.100.128.160
`ssh -l username 10.100.128.160` (公共用户public，密码public123)  

加载环境变量
$ module add bioinfo

对于计算量较大的任务，请不要在登录节点上直接运行，用qsub提交任务
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
尽量不要在登录节点（管理节点）上运行大型程序，ssh到其他计算节点上之后再运行其他程序。登录到10.100.128.160管理节点后，`ssh 计算节点名`，计算节点名可以是cu01, cu02, cu03, cu04, cu05, cu06  
推荐使用PBS作业管理系统提交任务，先将任务脚本存放在一个文件中，然后用`qsub`提交任务，下面是一个简单的任务`work.sh`, 任务的脚本文件work.sh中包含以下内容：  

```
#!/bin/bash
#PBS -S /bin/bash
#PBS -N JobName
#PBS -l nodes=1:ppn=1
#PBS -j oe
sleep 60
```

用`qsub`提交任务，`qstat`查看任务运行情况  

```
$ qsub work.sh
$ qstat
Job ID                    Name             User            Time Use S Queue
------------------------- ---------------- --------------- -------- - -----
217.mu01                   JobName          test03                 0 R batch          
218.mu01                   JobName          test03                 0 R batch          
219.mu01                   JobName          test03                 0 R batch    

$ qstat -n
Job ID                  Username    Queue    Jobname          SessID  NDS   TSK   Memory      Time    S   Time
----------------------- ----------- -------- ---------------- ------ ----- ------ --------- --------- - ---------
217.mu01                test03      batch    JobName           15970     1      1       --  7200:00:0 R  00:00:48
   cu06/0
218.mu01                test03      batch    JobName           15979     1      1       --  7200:00:0 R  00:00:48
   cu06/1
219.mu01                test03      batch    JobName           15995     1      1       --  7200:00:0 R  00:00:48
   cu06/2


```

**Linux学习资料**  
[Linux command line](https://github.com/hnnd/Linux_command_line)

**生物信息学非常有用的一行代码集成**  
      [Bioinformatics one-liners](https://github.com/hnnd/oneliners)
