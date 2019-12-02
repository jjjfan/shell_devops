# shell习题解析21_25.md
---  
## sar命令.md
[sar命令.md](sar命令.md)

## 【技巧】  
### 获取文件中的一行内容 
```  

line=`sed -n "$i"p a.txt`  #其中$i是变量行号  
```  
### 计算一行中的数字个数
    echo -n $line |sed 's/[^0-9]//g'|wc -L  
### md5sum命令得到的字符串一致，则说明两文件是内容一样的  
    md5sum a.txt
    md5sum b.txt
### 定义脚本接下来的输出将会写入到$LOG_FILE中
    exec >> $LOG_FILE 
### 杀死进程命令
    kill pid
    kill -9 pid  #强制杀死进程  
