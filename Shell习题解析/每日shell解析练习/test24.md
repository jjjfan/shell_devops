# 考试24.md  
---  
## 考试24  
1、写一个shell脚本，检测系统（CentOS7）所有普通用户家目录是否有更改过，比如user1默认家目录应该是/home/user1，如果user1的家目录改为了其它目录则说明user1家目录被改动过。   
   
## 【解答】   
```bash  
#!/bin/bash

usrList=`cat "/etc/passwd"| awk -F ':' '{ if ($3 >= 1000) print $1}'|grep -v "nobody"`
echo $usrList
for u in $usrList
do
       if [ ! -d /home/$u ]
       then
               echo ‘the $u home dir to be changed!’
       fi
done
```  

### 【答案】 
```bash  
#!/bin/bash
awk -F ':' '$3>=1000' /etc/passwd |while read line
do
    u_n=`echo $line|awk -F ':' '{print $1}'`
    u_h=`echo $line|awk -F ':' '{print $6}'`
    if [ $u_h == "/home/$u_n" ]
    then
        true
    else
        echo "$u_n 家目录被改动过"
    fi
done
```  



