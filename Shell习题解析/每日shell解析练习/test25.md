# 考试25.md  
---  
## 考试25  
1、公司里一部门有5人，写一个抓阄脚本，5选1，要求随机性。   
假设人员名单为：  
zhangsan  
lisi  
wangwu  
zhaoliu  
sunqi  

## 【解答】   
```bash  
#!/bin/bash

nameList='zhangsan lisi wangwu zhaoliu sunqi'
len=`echo $nameList|wc -L`
tt=$[$RANDOM+$len]
g_id=$[$tt%5]
if [ $g_id -eq 0 ]
then
        g_id=5
fi

echo "选择目标序号是 $g_id !"
k=0
for v in $nameList
do
        k=$[$k+1]
        if [ $k == $g_id  ]
        then
             echo "$v 是被选中的人员！"
        fi
done

``` 


### 【答案】 
```bash  
方法一：一条命令
假设人员名单文档ren.txt
shuf ren.txt |head -1


方法二：
#!/bin/bash
cat ren.txt|while read line
do
    name=$line
    n1=`echo $line|cksum|awk '{print $1}'`
    n=$[$n1*$RANDOM/$RANDOM/$RANDOM]
    echo $n $name
done  |sort -n -k 1 |sed -n '3'p |awk '{print $2}'


```  

