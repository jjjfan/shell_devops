# shell习题解析36_40.md
---  
## logrotate工具.md
[logrotate工具.md](logrotate工具.md)  

## 【技巧】  
#### 统计数字的个数
        sed 's/[^0-9]//g'|wc -L  
#### 逐行读取文件1.txt中内容到line中
        ```bash  
        while read line
        do 
            echo $line   
        done < 1.txt  
        ```  
#### for循环的倒序 for i in `seq 4 -1 1`  
#### 检测脚本错误 sh -n 1.sh 2>/tmp/sh.err 一旦发现错误，返回值$?是非零值 
#### 条件语法中：if [ $c == q ] || [ $c == Q ] 等同于 if [ $c == q -o $c == Q ]  #### 把字符串变为一行一个的形式 
        sed "s/[0-9]/&\n/g"  
#### 去除空格 和 最前面的","符号 sed 's/^,| //g'        