# 考试01.md  
---  
## 考试01  
        写一个shell脚本，计算/home/123/目录下所有文件大小，列出最大的20个文件并把结果写入到一个临时文件里，文件名字以年月日命名，比如/tmp/20190110.txt。  
【解答】  
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
### 【答案】  
```bash  
        #!/bin/bash
        find /home/123 -type f > /tmp/f.txt
        for f in `cat /tmp/f.txt`
        do
            du -sb $f
        done > /tmp/f_size.txt
        d=`date +%Y%m%d`
        sort -nr /tmp/f_size.txt |head -20 > /tmp/$d.txt

```  






