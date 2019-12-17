# shell习题解析79_84.md
---  
## iostat命令.md
[iostat命令.md](iostat命令.md)  


## 【技巧】  
### 删除指定目录$dir2下的7天前的日志文件
        find $dir2 -name "*.log" -type f -mtime +15 |xargs rm -f 
### 使用C语言的格式在for循环中以(( )) 的形式
        for((i=1;i<=$count;i++))
            do
                echo "$i"
            done       
### 查看磁盘io的负载，可以用 iostat -x 1 5 命令来看 %util 值，越高磁盘越忙，平均值一般不大于70 
    如果没有iostat 命令可以用 yum install -y sysstat 安装
    脚本里面判断是否存在iostat命令 
    if ! while iostat &>/dev/null
    then

    fi
### 使用awk 求和一列
    awk '{sum=sum+$NF} END {print sum}'  /tmp/1.log 
### 取得函数tr_24_12的输出用 $() 
    grep -n "$d_mdy $(tr_24_12 $2)" $logfile 
### 将24小时制时间转换为12小时
        tr_24_12()
        {
            date -d "$1" +%r
        }    
### 判断时间有效性
        judge_time()
        {
            date -d "$1" +%s &>/dev/null
            if [ $? -ne 0 ]
            then
                echo "你提供的时间$1格式不正确"
                exit 1
            fi
        }      
### 数组city=(1 2 3 a b 4)的输出
         echo ${city[$i]}  输出指定序号$i的数组元素  
         echo ${city[@]}  输出所有的数组元素  
         echo ${#city[@]}  输出数组的元素个数  
### 使用rsync 同步目录 $dir/下的文件，到机器 $B_ip上目录 $dir/下，不含logs目录       
    rsync -azP \
    --exclude="logs" \
     $dir/ $B_ip:$dir/
### 在read -p "是否要继续？(y|n)"后面未定义变量时候，默认被赋值到$REPLYZ中
### 在if[] 判断里面，-a 表示并且 -o表示或
        if [ $n -lt 2 -a $n -gt 10 ]
        then
            echo "条件 $n -lt 2 并且 $n -gt 10  "
        fi 

