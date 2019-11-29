# 使用shell脚本打印9x9乘法表.md
---   
## 1.使用for循环打印9x9乘法表：

###		示例1：
```bash  

        #!/bin/bash

        for ((  i=1;i<=9;i++  ))
        do
           for ((  j=1;j<=9;j++  ))
           do
              [  $j  -le  $i  ]  &&  echo -n "${i}*${j}=$((i*j))      "  
              #判断j是否小于i，当j大于i时不输出，输出不换行，末尾加一个制表符
           done
           echo ""           #输出一个换行符                
        done  
```
###		示例2：不做j与i大小的判断
```bash  

        #!/bin/bash
        for (( i=1;i<=9;i++ ))
        do
           for (( j=1;j<=9;j++ ))
           do
              echo -n "${i}*${j}=$((i*j))       "    #不做j与i的判断，结果将全部输出
           done
           echo ""
        done  
```

###		示例3：输出间隔不使用制表符，用空格替代
```bash  

        #!/bin/bash
        for (( i=1;i<=9;i++ ))
        do
           for (( j=1;j<=9;j++ ))
           do
              echo -n "${i}*${j}=$((i*j))    "   #使用空格替代制表符，输出结果无法对齐
           done
           echo ""
        done  
```

## 2.while循环打印9x9乘法表：

###		示例1：
```bash

        #!/bin/bash
        i=1
        j=1
        while [ $i -lt 10 ]
        do
           while [ $j -lt 10 ]
           do
             [ $j -le $i ] &&  echo -n "$i*$j=$((i*j))  "
             let j++
           done
           let i++
           let j=1       #将j重新赋值为1，否则除第一行外后续将全部空行，原因是经过上一次循环后j已不在小于10
           echo ""
        done  
```

###		示例2：去掉let  j=1  ，去掉后除第一行外全部输出空行  
```bash  

        #!/bin/bash
        i=1
        j=1
        while [ $i -le 9 ]
        do
           while [ $j -le 9 ]
           do
             [ $j -le $i ] &&  echo -n "$i*$j=$((i*j))  "
             let j++
           done
           let i++
           echo ""
        done
```
## 3.while结合for循环，打印9x9乘法表：  
```bash  
  
        #!/bin/bash
        i=1
        while [ $i -le 9 ]
        do
           for (( j=1;j<=9;j++ ))
           do
             [ $j -le $i ] && echo -n "$i*$j=$((i*j))   "
           done
           echo ""
           let i++
        done
```  