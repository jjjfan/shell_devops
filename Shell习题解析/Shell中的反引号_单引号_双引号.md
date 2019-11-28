# Shell中的反引号_单引号_双引号.md  
---  
## 反引号  
        反引号位 (`) 位于键盘的Tab键的上方、1键的左方。  
        注意与单引号(')位于Enter键的左方的区别。  
        在Linux中起着命令替换的作用。命令替换是指shell能够将一个命令的标准输出插在一个命令行中任何位置。  
        反引号可以表示一个命令的结果，通常给变量赋值。
        如下，shell会执行反引号中的date命令，把结果插入到echo命令显示的内容中。  

        [root@localhost sh]# echo The date is `date`   
        The date is 2011年 03月 14日 星期一 21:15:43 CST   
        [root@localhost sh]#n=`wc -l /etc/passwd|awk '{print $1}'`  
        [root@localhost sh]#echo $n    
        23    

## 单引号、双引号用于用户把带有空格的字符串赋值给变量事的分界符。 
```  
        [root@localhost sh]# str="Today is Monday"  
        [root@localhost sh]# echo $str  
        Today is Monday  
        如果没有单引号或双引号，shell会把空格后的字符串解释为命令。  
        [root@localhost sh]# str=Today is Monday  
        bash: is: command not found  
```  
## 单引号和双引号的区别。
```  
        单引号告诉shell忽略所有特殊字符，而双引号忽略大多数，但不包括$、\、`。
        [root@localhost sh]# testvalue=100  
        [root@localhost sh]# echo 'The testvalue is $testvalue'  
        The testvalue is $testvalue  
        [root@localhost sh]# echo "The testvalue is $testvalue"  
        The testvalue is 100  
```  
## 总结  
        1.在shell脚本中使用反引号时，他本身就对\做了一层转义，如果你有需要匹配的\的情况的话，需要再次进行转义。所以在反引号中，两个转义符才是进行转义！  
        2.$()中则不需要考虑\的问题，与我们平常使用的一样：\ = \。且自己转义后，他还是识别转义符。  
        3.反引号是老的用法，$()是新的用法，我们推荐使用$()。  



