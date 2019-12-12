# shell习题解析61_66.md
---  
## curl命令.md
[curl命令.md](curl命令.md)  
## split命令.md
[split命令.md](split命令.md) 



## 【技巧】  
### grep -f 选项支持把一个文件的内容作为匹配对象  
### 精确匹配整行的内容 grep -q "^$line$" b.txt  
### 匹配a.txt 和b.txt 中都有的行 grep -wf b.txt a.txt  
### 匹配a.txt中有，但是b.txt中 没有的行 grep -vwf b.txt a.txt  
### 当前用户的用户名变量 $USER  
### 匹配最后一列含有august关键字的行，打印出来第一列
    awk '$NF ~ /august/ {print $1}'   
### 当前主机的CPU生产商，其信息在/proc/cpuinfo文件中vendor id一行中
        如果其生产商为AuthenticAMD，就显示其为AMD公司；
        如果其生产商为GenuineIntel，就显示其为Intel公司；
        否则，就说其为非主流公司。