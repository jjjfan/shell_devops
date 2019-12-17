# 考试23.md  
---  
## 考试23  
1、服务器上有一个图片目录(/data/images)需要备份，写一个备份脚本，首先计算整个图片目录的大小，然后判断该图片目录是否能备份到本机最大的磁盘分区下，如果能直接备份，不能则告诉脚本执行者无法备份。

## 【解答】   


#!/bin/bash

getDirSize()
{
        decDir=$1
        if [ -n $decDir ]
        then
                decDir="."
        fi

        #echo "decDir is $decDir"
        dirSize=`du -sm $decDir`
        echo $dirSize |awk '{print $1}'
}

getMaxDisk()
{
        decDir=`df -hm |grep -v "Use%"|awk -F ' +|% +'  ' { print $4,$6} '|sort -nr |head -1|awk '{print $2}'`
        decSize=`df -hm |grep -v "Use%"|awk -F ' +|% +'  ' { print $4,$6} '|sort -nr |head -1|awk '{print $1}'`
        echo "decDir is $decDir"
        echo "decSize is $decSize"

        if [ $1 -gt $decSize  ]
        then
                echo "disk is small !can not to backup!"
                exit 1
        fi
        echo $decDir
}


#getDirSize "/data/images"
dirSize=`getDirSize`

bakDir=`getMaxDisk $dirSize`

#tar czPf data_images.tar.gz /home/ubaugust/
tar czPf $bakDir/data_images.tar.gz /data/images/

```  


### 【答案】 
```bash  
#!/bin/bash
dir="/data/images"
s1=`du -sk $dir |awk '{print $1}'`

df -k |sort -n -k 4 |tail -1 > /tmp/df.log
s2=`awk '{print $4}' /tmp/df.log`

bigdir=`awk '{print $NF}' /tmp/df.log`

if [ $s2 -gt $s1 ]
then
    rsync -a $dir/ $bigdir/images_bak/
else
    echo "磁盘空间不够，无法备份。"
fi

```  


