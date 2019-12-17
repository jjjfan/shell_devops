# 考试26.md  
---  
## 考试26  
    1、数据库db1里有一个tb1表，其中number字段每秒钟生成一个数字，用shell脚本计算number字段每分钟的平均值，要求在任何时间执行该脚本都可以返回过去1分钟内的平均数。  
    假设：  
    1）用户名：user1 密码：user1-pass

## 【解答】   
通过sql语句查询与当前时间相隔5分钟以内的数据。
select * from 数据表名 where 字段名 between date_add(now(), interval - 5 minute) and now();
字段名是字符串格式，也是可以的。

```bash  
#!/bin/bash
mysqlc="/usr/bin/mysql -uuser1 -puser1-pass db1
$mysqlc -e "select number from tb1 between date_add(now(),interval - 1 minute) and now()" > nlist.txt
ll=`wc -l nlist.txt|awk '{print $1}'`
avg=`sed -n '2,'$[$ll-1]"'p" nlist.txt |awk  '{{tot=tor+$1};END { print tot/60} }'`
echo '过去一分钟的平均值为 $avg ！'

```  
### 【答案】 
```bash  
#!/bin/bash
mys=”mysql -uuser1 -p’user1-pass’“
n=$mys db1 -e "select count(*) from tb1" |tail -1
n1=$[$n-60]
$mys db1 -e “select number from tb1 limit $n1, 60” |sed  “1”d > /tmp/number.txt

awk ‘{sum+=$1} END { print sum/NR}’ /tmp/number.txt


```  


