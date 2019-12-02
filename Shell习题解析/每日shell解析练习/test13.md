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
        mail=123@123.com
        log=/data/logs/error.log
        #log=/tmp/20191128.txt
        stline=`sed -n '$=' $log`
        #echo $stline

        curline=0
        while :
        do
                curline=`sed -n '$=' $log`
                #echo "curline while $curline"
                #echo "stline while $stline"
                
                clrflag=`date +%T|awk -F ':' '{if ($1==0 && $2==$1) {print $1}}'`
                #clrflag=`date +%T|awk -F ':' '{if ($1==10 && $2==47) {print 0}}'`
                
                if [ $clrflag -eq 0 ]
                then
                        curline=$((0))
                        stline=$((0))
                #       echo "clear flag"
                fi
                
                dif=$((curline-stline))
                echo "dif is $dif"
                if [ $dif -gt 0 ];
                then
                        stline=$curline
                #       echo "gt $stline"
                        python /usr/local/sbin/mail.py $mail "new error log" "`$date +%F %T` log new error"
                fi
        #       echo "while done"
                sleep 10
        done

```  

