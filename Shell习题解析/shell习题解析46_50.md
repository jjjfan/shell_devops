# shell习题解析46_50.md
---  

## 【技巧】  
### 以冒号“：”分隔过滤出数字开头的行，打印出第二列  
ip add |awk -F ': ' '$1 ~ "^[1-9]" {print $2}'  
### 指定网卡名字eth0获取到所有的IP地址 
    ip add show dev eth0 |grep inet |awk '{print $2}' |awk -F '/' '{print $1}'
### 系统中存在的IP地址  
    ip add |grep inet |awk '{print $2}'|awk -F '/' '{print $1}'|xargs  
### 去除数组输出间的空格 echo ${a[@]}|sed s'/ //g'  
### 查找指定的进程 ps -C "$name"  
### 获取输入参数字符串的长度  $[#1]
### 获取指定字符串中的指定子串 如：
        echo ${1:4:2} 获取参数1中的第四和五的字符  
        echo ${datenum:0:4} 获取$datenum的前四位字符  
### 去除小数点 sed 's/\.//g'  
        