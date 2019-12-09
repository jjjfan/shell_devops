# 考试14.md  
---  
## 考试14  
        用shell脚本打印乘法口诀。

## 【解答】   
```bash  

        #!/bin/bash
        for i in `seq 1 9`
        do
                for j in `seq 1 9`
                do
                        [ $j -le $i ] && echo -n "$j * $i =  $((i*j))    "   #一行内连续，空格分开
                done
                echo ""  #换行
        done


```  

### 【答案】 
```bash  
for i in `seq 1 9`; do for j in `seq 1 $i`; do echo -n "$i*$j=$[$i*$j] "; done;echo;  done 
```  