# shell中的条件判断.md
---  
## 一. 具体每个选项对应的判断内容:
```  
    -e filename 如果 filename存在，则为真 
    -d filename 如果 filename为目录，则为真 
    -f filename 如果 filename为常规文件，则为真 
    -L filename 如果 filename为符号链接，则为真 
    -r filename 如果 filename可读，则为真 
    -w filename 如果 filename可写，则为真 
    -x filename 如果 filename可执行，则为真 
    -s filename 如果文件长度不为0，则为真 
    -h filename 如果文件是软链接，则为真
```  
## 二.常用的例子:
### 1.判断文件夹是否存在
```  
    #shell判断文件夹是否存在
    #如果文件夹不存在，创建文件夹
    if [ ! -d "/myfolder" ]; then
      mkdir /myfolder
    fi 
```  
### 2.判断文件夹是否存在并且是否具有可执行权限
```  
    #shell判断文件,目录是否存在或者具有权限
    folder="/var/www/"
    file="/var/www/log"

    # -x 参数判断 $folder 是否存在并且是否具有可执行权限
    if [ ! -x "$folder"]; then
      mkdir "$folder"
    fi
```  
### 3.判断文件夹是否存在
```  
 # -d 参数判断 $folder 是否存在
 if [ ! -d "$folder"]; then
   mkdir "$folder"
 fi
```   
### 4.判断文件是否存在
```  
     # -f 参数判断 $file 是否存在
     if [ ! -f "$file" ]; then
       touch "$file"
     fi
```   
### 5.判断一个变量是否有值
```  
# -n 判断一个变量是否有值
if [ ! -n "$var" ]; then
  echo "$var is empty"
  exit 0
fi
```  
### 6.判断两个变量是否相等.
```  
# 判断两个变量是否相等
if [ "$var1" = "$var2" ]; then
  echo '$var1 eq $var2'
else
  echo '$var1 not eq $var2'
fi
```  
### 7.判断count变量是否为空，是否为数字.
```  
        if [ -z "$count"  ]
        then
                count=21
             # echo "in -z $count"
        elif echo $count | grep -q '[^0-9]'
        then
                count=21
              #echo "in -n $count"
        else
               count=$[$count+1]
              #echo "aaa $count"
        fi
```  