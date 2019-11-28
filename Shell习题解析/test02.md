# 考试02.md  
---  
## 考试02  
        写一个shell脚本，每隔30秒查看一次日志文件/data/logs/error.log，看有没有产生新的日志，如果有产生新日志，需要发邮件告警。  
        假设：  
        1）该日志0点0分会被清空。  
        2）邮件脚本路径/usr/local/sbin/mail.py  
        思路：  
        while循环，sleep30  
        判断时间点，如果是0点0分需考虑特殊情况  
        记录上一次日志的行数，对比本次日志行数和上一次日志行数  
## 【解答】  
```       
        #!/bin/bash    
        dest=    
        count=$2    
        #echo "ls target dir is $dest !!!"  
        #echo "top size num is $2 !!!"  
        if [ -z "$1"  ]  
        then  
                dest="/home/123/"  
        else  
                dest=$1  
        fi  

        if [ -z "$count"  ]  
        then  
                count=21  
             # echo "in -z $count"  
        elif echo $count | grep -q '[^0-9]'  
        then  
                count=21  
              #echo "in -n $count"  
        else  
               count=$[$count+1]  
              #echo "aaa $count"  
        fi  

        #echo "bbb $count"  
        sum=0  
        d=`date +%Y%m%d`  
        logfile=/tmp/$d.txt  

        if [ -d "$dest"  ]  
        then  
                echo "ls target dir is $dest !!!"  
                echo "top size num is $[$count-1] !!!"  
                ls -al $dest > $logfile  
        else  
                dest="."  
                echo "ls target dir is $dest to current dir !!!"  
                echo "top size num is $[$count-1] !!!"  
                ls -al . > $logfile  
        fi  
        sed -i '1,3'd $logfile  
        sort -k5rn $logfile -o $logfile  
        #cat $logfile  
        for s in `cat $logfile |awk '{print $5}'`  
        do  
                sum=$[$sum + $s]  
        done  

        echo "the total file size is $sum !"  
        sed -i $count',$d' $logfile   
```  

