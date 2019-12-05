# shell习题解析31_35.md
---  

## 【技巧】  
#### 通过指定网卡获取ip  
ip addr show eth0  
#### 判断参数的个数 [ $# -eq 0 ]  
#### 遍历参数 for d in $@  或是 for i in `seq 1 $#`
#### shell中不支持“$$i”这样的写法，比如n=3.要表示$3，echo $$n是不成立的
需要特殊处理为： a=$n; echo $(!a)  
#### 在case语句中，选项里面的变量值可以有多个，用“|”做分割符
case $c in 
    y|Y)
    ;;
#### 判断命令是否执行成功 看$?是否为0
    if [ $? -eq 0 ]
    then
        exit 0
    else
        echo "下载失败."
        exit 52
    fi    
#### 产生随机数 n=$[$RANDOM%101] 或是 m=`echo $RANDOM;n1=$[$m%100]` (1到99随机数字)  
#### 判断字符串中字符只能是大小写字符、数字，不能有其他的特殊符号  
        u1=`echo $u|sed 's/[a-zA-Z0-9]//g'`  
        if [ -n "$u1" ]  
        或是  
        if echo $name |gep -q '[a-zA-Z0-9]'  
#### 检索 $f 中 第一列和$u 相同的行，并打印出对应的第二列
        awk -v uu=$u '$1==uu {print $2}' $f         
#### 列出最大的文件的大小和所在行号  
        ll |grep -v 'total' |awk -v uu=0 '$5>uu {uu=$5} END{print uu,NF}'  
        

