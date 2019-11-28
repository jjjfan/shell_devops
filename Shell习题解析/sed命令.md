# sed命令.md
---  
#### sed -i '1,3'd $logfile 
    删除文件的 1到3行
#### sed -i $count',$d' $logfile
    删除 变量count值代表的行 到文件的最后一行

## sed命令行格式为：
         sed [-nefri]  ‘command’  输入文本/文件       

### 常用选项：
        -n∶取消默认的输出,使用安静(silent)模式。在一般 sed 的用法中，所有来自 STDIN的资料一般都会被列出到屏幕上。但如果加上 -n 参数后，则只有经过sed 特殊处理的那一行(或者动作)才会被列出来
        -e∶进行多项编辑，即对输入行应用多条sed命令时使用. 直接在指令列模式上进行 sed 的动作编辑
        -f∶指定sed脚本的文件名. 直接将 sed 的动作写在一个档案内， -f filename 则可以执行 filename 内的sed 动作
        -r∶sed 的动作支援的是延伸型正则表达式的语法。(预设是基础正则表达式语法)
        -i∶直接修改读取的文件内容，而不是由屏幕输出      

### 常用命令：
         a ∶ 新增， a 的后面可以接字串，而这些字串会在新的一行出现(目前的下一行)
         c ∶ 取代， c 的后面可以接字串，这些字串可以取代 n1,n2 之间的行
         d ∶ 删除，因为是删除，所以 d 后面通常不接任何内容
         i ∶ 插入， i 的后面可以接字串，而这些字串会在新的一行出现(目前的上一行)
         p∶ 列印，亦即将某个选择的资料印出。通常 p 会与参数 sed -n 一起用
         s∶ 取代，可以直接进行替换的工作。通常这个 s 的动作可以搭配正则表达式。例如 1,20s/old/new/g 
### sed命令的调用:
    在命令行键入命令;将sed命令插入脚本文件,然后调用sed;将sed命令插入脚本文件,并使sed脚本可执行
    sed [option] sed命令 输入文件            在命令行使用sed命令,实际命令要加单引号
    sed [option] -f sed脚本文件 输入文件     使用sed脚本文件
    sed脚本文件 [option] 输入文件            第一行具有sed命令解释器的sed脚本文件
    option如下:
      n 不打印; sed不写编辑行到标准输出,缺省为打印所有行(编辑和未编辑),p命令可以用来打印编辑行
      c 下一命令是编辑命令,使用多项编辑时加入此选项
      f 如果正在调用sed脚本文件,使用此选项,此选项通知sed一个脚本文件支持所用的sed命令,如
          sed -f myscript.sed input_file  这里myscript.sed即为支持sed命令的文件
    使用重定向文件即可保存sed的输出

### 使用sed在文本中定位文本的方式:
    x       x为一行号,比如1
    x,y     表示行号范围从x到y,如2,5表示从第2行到第5行
    /pattern/    查询包含模式的行,如/disk/或/[a-z]/
    /pattern/pattern/   查询包含两个模式的行,如/disk/disks/
    /pattern/,x  在给定行号上查询包含模式的行,如/disk/,3
    x,/pattern/  通过行号和模式查询匹配行,如 3,/disk/
    x,y!    查询不包含指定行号x和y的行

### 基本sed编辑命令:
    p      打印匹配行                      c/    用新文本替换定位文本
    =      显示文件行号                    s     使用替换模式替换相应模式
    a/     在定位行号后附加新文本信息        r     从另一个文本中读文本
    i/     在定位行号后插入新文本信息        w     写文本到一个文件
    d      删除定位行                      q     第一个模式匹配完成后退出或立即退出
    l      显示与八进制ASCII代码等价的控制字符        y  传送字符
    n      从另一个文本中读文本下一行,并附加在下一行   {}     在定位行执行的命令组
    g      将模式2粘贴到/pattern n/

         
## sed命令补充 
如果在变量a或者b有 -、/ 等特殊字符，则需要用 \ 进行转义
字符串变量中可以用单引号或者双引号 ，区别：双引号支持变量引用、转义符（比如\n 换行），单引号不支持
sed 命令执行时加 -i 参数会把修改应用到源文件上，否则只是屏幕显示
```  
a="one"
b="two"
# 第一种：
eval sed -i ’s/$a/$b/’ filename
# 第二种（推荐）：
sed -i "s/$a/$b/" filename
# 第三种：
sed -i ’s/’$a’/’$b’/’ filename 
# 第四种：
sed -i s/$a/$b/ filename
```  

## 基本sed编程举例:
    使用p(rint)显示行: sed -n '2p' temp.txt   只显示第2行,使用选项n
    打印范围:  sed -n '1,3p' temp.txt         打印第1行到第3行
    打印模式:  sed -n '/movie/'p temp.txt     打印含movie的行
    使用模式和行号查询:  sed -n '3,/movie/'p temp.txt   只在第3行查找movie并打印
    显示整个文件:  sed -n '1,$'p temp.txt      $为最后一行
    任意字符:  sed -n '/.*ing/'p temp.txt     注意是.*ing,而不是*ing
    打印行号:  sed -e '/music/=' temp.txt
    附加文本:(创建sed脚本文件)chmod u+x script.sed,运行时./script.sed temp.txt
        #!/bin/sed -f
        /name1/ a/             #a/表示此处换行添加文本
        HERE ADD NEW LINE.     #添加的文本内容
    插入文本: /name1/ a/ 改成 4 i/ 4表示行号,i插入
    修改文本: /name1/ a/ 改成 /name1/ c/ 将修改整行,c修改
    删除文本: sed '1d' temp.txt  或者 sed '1,4d' temp.txt
    替换文本: sed 's/source/OKSTR/' temp.txt     将source替换成OKSTR
             sed 's//$//g' temp.txt             将文本中所有的$符号全部删除
             sed 's/source/OKSTR/w temp2.txt' temp.txt 将替换后的记录写入文件temp2.txt
    替换修改字符串: sed 's/source/"ADD BEFORE" &/p' temp.txt
             结果将在source字符串前面加上"ADD BEFORE",这里的&表示找到的source字符并保存
    sed结果写入到文件: sed '1,2 w temp2.txt' temp.txt
                     sed '/name/ w temp2.txt' temp.txt
    从文件中读文本: sed '/name/r temp2.txt' temp.txt
    在每列最后加文本: sed 's/[0-9]*/& Pass/g' temp.txt
    从shell向sed传值: echo $NAME | sed "s/go/$REP/g"   注意需要使用双引号

## 定址
    定址用于决定对哪些行进行编辑。地址的形式可以是数字、正则表达式、或二者的结合。如果没有指定地址，sed将处理输入文件的所有行。
    地址是一个数字，则表示行号；是“$"符号，则表示最后一行。例如： 
```  
    sed -n '3p' datafile
    只打印第三行
```  
    只显示指定行范围的文件内容，例如：
```  
# 只查看文件的第100行到第200行
sed -n '100,200p' mysql_slow_query.log
```  
    地址是逗号分隔的，那么需要处理的地址是这两行之间的范围（包括这两行在内）。范围可以用数字、正则表达式、或二者的组合表示。例如：
```  
    sed '2,5d' datafile
    #删除第二到第五行
    sed '/My/,/You/d' datafile
    #删除包含"My"的行到包含"You"的行之间的行
    sed '/My/,10d' datafile
    #删除包含"My"的行到第十行的内容
```  
## 替换：
    -e是编辑命令，用于sed执行多个编辑任务的情况下。在下一行开始编辑前，所有的编辑动作将应用到模式缓冲区中的行上。  
```  
    sed -e '1,10d' -e 's/My/Your/g' datafile  
    #选项-e用于进行多重编辑。第一重编辑删除第1-3行。第二重编辑将出现的所有My替换为Your。因为是逐行进行这两项编辑（即这两个命令都在模式空间的当前行上执行），所以编辑命令的顺序会影响结果。  
    # 替换两个或多个空格为一个空格  
    sed 's/[ ][ ]*/ /g' file_name  
    # 替换两个或多个空格为分隔符:  
    sed 's/[ ][ ]*/:/g' file_name  
    # 如果空格与tab共存时用下面的命令进行替换  
    # 替换成空格  
    sed 's/[[:space:]][[:space:]]*/ /g' filename  
    # 替换成分隔符:  
    sed 's/[[:space:]][[:space:]]*/:/g' filename      
```  
