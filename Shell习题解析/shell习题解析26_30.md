# shell习题解析26_30.md
---  

## 【技巧】  
### 判断日志文件中的内容时候，可以先判断文件是否有内容行数，没有则无需判断内容的正确与否
```  
# 变量$n1为文件的行数
if [$n1 -gt 0]
then  
    echo "do something!!!"
fi  

```  
### 取得变量值、变量运算在ubuntu 和 centos 上有区别  
    ubuntu  使用 $(())来获取： a=$((a+1))  
    centos  使用 $[] 来获取： a=$[$a+1]  
### 循环for 的使用
    for i in  {1..100}  等同于 for i in `seq 1 100`
### 保留两位小数  
    a=10;b=3;echo "scale=2;$a/$b"|bc
### 取得参数个数 $#
### 判断变量是否是整数的方法 grep '[^0-9]'  
### 判断字符串相等使用 == 不能使用 -eq  

