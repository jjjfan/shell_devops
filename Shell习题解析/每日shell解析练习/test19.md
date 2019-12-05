# 考试19.md  
---  
## 考试19  
    1、有5台服务器A、B、C、D、E，其中A为其余4台机器的跳板机。即，A可以直接ssh免密码登录B、C、D、E。
    写一个脚本，实现如下需求：  
    1）假设A机器上的时间是正确的  2）依次检查B、C、D、E机器上的时间，如果时间和A机器相差超过2秒，则需要同步一下时间  3）同步时间的命令为：ntpdate time.windows.com   
    4）假设所有机器上都有ntpdate命令  

## 【解答】   
```bash  

#!/bin/bash
A_ip="123.45.67.89"
B_ip="123.45.67.89"
C_ip="123.45.67.89"
D_ip="123.45.67.89"
E_ip="123.45.67.89"

A_user="root"
A_passwd="123456"
A_time=`ssh $A_ip "date +%s" `
B_time=`ssh $A_ip "ssh $B_ip 'date +%s' " `
if [ $((A_time-B_time)) -gt 2 ] ||  [ $((A_time-B_time)) -lt -2 ]
then
        ssh $A_ip "ssh $B_ip 'ntpdate time.windows.com' "
fi

A_time=`ssh $A_ip "date +%s" `
C_time=`ssh $A_ip "ssh $C_ip 'date +%s' " `
if [ $((A_time-C_time)) -gt 2 ] ||  [ $((A_time-C_time)) -lt -2 ]
then
        ssh $A_ip "ssh $C_ip 'ntpdate time.windows.com' "
fi

A_time=`ssh $A_ip "date +%s" `
D_time=`ssh $A_ip "ssh $D_ip 'date +%s' " `
if [ $((A_time-D_time)) -gt 2 ] ||  [ $((A_time-D_time)) -lt -2 ]
then
        ssh $A_ip "ssh $D_ip 'ntpdate time.windows.com' "
fi

A_time=`ssh $A_ip "date +%s" `
E_time=`ssh $A_ip "ssh $E_ip 'date +%s' " `
if [ $((A_time-E_time)) -gt 2 ] ||  [ $((A_time-E_time)) -lt -2 ]
then
        ssh $A_ip "ssh $E_ip 'ntpdate time.windows.com' "
fi


```  
