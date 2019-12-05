# 考试21.md  
---  
## 考试21  
1、分别用awk和shell计算1.txt最后一列（用空白字符分隔）数字的平均值   

## 【解答】   
``` bash   

awk -F' ' '{ tot=tot+$(NF);num=num+1 } END { print tot/num }' 1.txt
或
#!/bin/bash
num=`cat 1.txt |wc -l `
tot=0
n=0
for i in `cat 1.txt|awk '{print $NF}'`
do
        if [ -z $n ]
        then
                n=0
        fi
        tot=$[$tot+$i]
done
echo $num
avg=`echo 'scale=2; '$tot/$num'' |bc`

echo "avg : $avg"


```  