# shell判断变量是字符还是数字.md
--- 
## 1、通过grep去筛选非数字，判断其输出状态，以下两种方式：  
```  
 #!/bin/bash
 read -p "please input a num: "  num
 if echo $num | grep -q '[^0-9]'
 then
         echo "this is not a num,please input num"
         exit 1
 fi
``` 

```  
#!/bin/bash
read -p "please input a num: "  num
echo $num | grep -q '[^0-9]'
n1=$?
if [ $n1 -eq 0 ]
then
        echo "this is not a num,please input num"
        exit 1
fi
```  

## 2、通过用 sed 's///g'替换的方式，把数字替换为null，然后去判断输出是否为null，如果不为null，则说明有字符啦  
```bash  

#!/bin/bash
read -p "please input a num: "  num
n1=`echo $num|sed 's/[0-9]//g'`
if [ ! -z $n1 ]
then
        echo "this is not a num,please input num"
        exit 1
fi

```  
```bash  

#!/bin/bash
read -p "please input a num: "  num
n1=`echo $num|sed 's/[0-9]//g'`
if [ -n "$n1" ]
then
        echo "this is not a num,please input num"
        exit 1
fi

```  
