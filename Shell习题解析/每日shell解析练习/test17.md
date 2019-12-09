# 考试17.md  
---  
## 考试17  
    1、服务器上有一个目录/abc/123/images/，下面有按照每天日期命名的目录，如day_20181010。写一个脚本，把/abc/123/images/下面的2017年全年的目录打包压缩，如day_20170108压缩后为day_20170108.tar.gz，并删除掉day_20170108目录。


## 【解答】   
```bash  

#!/bin/bash
destdir=
destyear=$2
#echo "ls target dir is $dest !!!"
#echo "top size num is $2 !!!"
if [ -z "$1"  ]
then
        destdir="/abc/123/images/"
elif [ -d "$1"   ]
then
        destdir=$1
else
        destdir="/abc/123/images/"
fi

if [ -z "$destyear"  ]
then
        destyear=2017
      echo "in -z "
elif echo $destyear | grep -q '[^0-9]'
then
        destyear=2017
      echo "in -n grep -q"
fi

#echo $destdir
#echo $destyear

cd $destdir
#echo `pwd`
for logdir in `find . -type d -name "day_"$destyear'*' | sed 's/[^0-9]//g'`
do
        #echo "$logdir"
        #echo `pwd`
        tar -czvf "day_"$logdir.tar.gz  "./day_"$logdir"/" &>/dev/null
        rm -rf  "day_"$logdir"/"
done
```  
### 【答案】 
```bash  
        #!/bin/bash
        cd  /abc/123/images
        for d in `ls day_2017*`
        do
            tar zxf $d.tar.gz $d && rm -rf $d
        done

```  