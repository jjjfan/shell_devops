# 考试20.md  
---  
## 考试20  
    1、写一个支持带参数的shell脚本，查询MySQL指定库和指定表的数据。具体要求如下：   
        1）用户执行脚本格式不对时，需要提示用户正确的脚本用法  2）第一个参数指定数据库名，必须指定  
        4）第二个指定表名，必须指定  5）第三个参数指定查询多少行（前N行），可以不指定（如果不指定，就查询所有行）   假设：mysql root用户密码为dil72lVBn  

## 【解答】   
```bash  

#!/bin/bash
tag=0
dbname=
tbname=
linenum=0

Mysql_c="mysql -uroot -pdil72lVBn"
if [ $# -lt 2 ]
then
        tag=-1
elif [ $# -eq 2 ]
then
        tag=1
elif [ $# -eq 3 ]
then
        tag=2
        if echo $3|grep -q '[^0-9]'
        then
                tag=-2
                echo $tag
        fi
else
        tag=0
fi

dbname=$1
tbname=$2
linenum=$3
echo "$dbname.$tbname head $linenum"
case $tag in
        1)
                echo "list all line"
                #echo "$Mysql_c -e "select * from $dbname.$tbname""
                $Mysql_c -e "select * from $dbname.$tbname"
                ;;
        2)
                echo "list $3 line!!!"
                #echo "$Mysql_c -e "select * from $dbname.$tbname limit $linenum ""
                $Mysql_c -e "select * from $dbname.$tbname limit $linenum "

                ;;
        0)
                echo "to many parameter!"
                echo "./test20.sh databasename tablename  [ headlinenum  ]"
                ;;
        *)
                echo "to less parameter!"
                echo "./test20.sh databasename tablename  [ headlinenum  ]"
esac
echo "===== end ====="

```  
### 【答案】 
```bash  

#!/bin/bash
mys="mysql -uroot -pdil72lVBn"

if [ $# -ne 2 ] && [ $# -ne 3 ]
then
    echo "Please use: sh $0 databasename tablename [count]"
    exit 1
fi

$mys -e "show databases"|sed '1'd > /tmp/databases.txt
if ! grep -qw "$1" /tmp/databases.txt
then
    echo "sorry, there is no database $1."
    exit 1
fi

$mys $1 -e  "show tables"|sed '1'd > /tmp/$1_tables.txt
if ! grep -qw "$2" /tmp/$1_tables.txt
then
    echo "sorry, there is no table $2."
    exit 1
fi

if [ -n "$3" ]
then
    $mys $1 -e "select * from $2 limit $3"
else
    $mys $1 -e "select * from $2"
fi
```  
