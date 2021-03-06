# shell脚本参数获取.md  
---  
## Linux中变量$[#,@,0,1,2,*,$,?]含义  
```  
$# 是传给脚本的参数个数
$0 是脚本本身的名字
$1 是传递给该shell脚本的第一个参数
$2 是传递给该shell脚本的第二个参数
$@ 是传给脚本的所有参数的列表
$* 是以一个单字符串显示所有向脚本传递的参数，与位置变量不同，参数可超过9个
$$ 是脚本运行的当前进程ID号
$? 是显示最后命令的退出状态，0表示没有错误，其他表示有错误
```  
## shell中$*与$@的区别
    关于$* 和 $@的 一点 认识 同是菜鸟一起学习

###    $*
    所有的位置参数,被作为一个单词.
    注意:"$*"必须被""引用.
###    $@
    与$*同义,但是每个参数都是一个独立的""引用字串,这就意味着参数被完整地传递,
    并没有被解释和扩展.这也意味着,每个参数列表中的每个参数都被当成一个独立的
    单词.
    注意:"$@"必须被引用.

###    $@ $* 只在被双引号包起来的时候才会有差异
    双引号括起来的情况：
    $*将所有的参数认为是一个字段
    $@以IFS（默认为空格）来划分字段，如果空格在“”里面，不划分。

    采用LS的脚本运行./test 1 "2 3" 4   来发现差异
    没有括起来的情况是$@和$*一样的，见到IFS就划分字段。
    还是采用LS的脚本运行./test 1 "2 3" 4   来发现差异
###     相同点：都是引用所有参数
###     不同点：  
####        $* 和 $@ 都表示传递给函数或脚本的所有参数，不被双引号(" ")包含时，都以"$1" "$2" … "$n" 的形式输出所有参数。  
####        但是当它们被双引号(" ")包含时，"$*" 会将所有的参数作为一个整体，以"$1 $2 … $n"的形式输出所有参数；"$@" 会将各个参数分开，以"$1" "$2" … "$n" 的形式输出所有参数。  

---  
```  
        #!/bin/bash  
        echo "-----------------"  
        for key in "$@"  
        do  
            echo '$@' $key  
        done  
        echo "-----------------------------"  
        for key2 in $*  
        do  
            echo '$*' $key2  
        done  

        1、带引号执行及结果：   
        [root@localhost ~]# bash file.sh linux "python c"  
        -----------------  
        $@ linux  
        $@ python c  
        -----------------------------  
        $* linux  
        $* python  
        $* c  
        2、不带引号执行及结果：   
        [root@localhost ~]# bash file.sh linux python c  
        -----------------  
        $@ linux  
        $@ python  
        $@ c  
        -----------------------------  
        $* linux  
        $* python  
        $* c  

```  
