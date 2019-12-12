# bc命令.md  
---  
## bc 命令是任意精度计算器语言，通常在linux下当计算器用。   
## 常用的运算：  
        * 加法
        + 减法
        - 乘法
        / 除法
        ^ 指数
        % 余数
## 语法  
        bc(选项)(参数)
## 选项值  
        --help  -h 显示指令的帮助信息。
        --interactive -i 使用交互模式,强制进入交互式模式；
        --mathlib  -l 执行指定语句前，先加载math函数库,定义使用的标准数学库
        --warn  -w 对非POSIX的bc指令给出警告
        --standard  -s 启动POSIX模式下的bc程序
        --quiet  -q 不显示GNU bc 的欢迎,不打印正常的GNU bc环境信息
        --version  -v 显示版本信息
## 参数  
        文件：指定包含计算任务的文件。   
## 是什么,怎么用
    bc - An arbitrary precision calculator language   一个任意精度的计算器语言。
    从他的使用上来看，能够对计算公式的语法进行解释并返回出结果。有下面几种使用方式:
### 交互式  
    输入bc，进入交互式界面，然后输入3+1，回车后在下一行打印出了4  
### echo+管道  
    echo "3+1" | bc 返回4到屏幕上
    scale=2 设小数位，2 代表保留两位:
    $ echo 'scale=2; (2.777 - 1.4744)/1' | bc
    1.30
    bc 除了 scale 来设定小数位之外，还有 ibase 和 obase 来其它进制的运算:
    $ echo "ibase=2;111" |bc
    7
    abc=11000000 
    echo "obase=10;ibase=2;$abc" | bc
    执行结果为：192，这是用bc将二进制转换为十进制。
    操作基本都是围绕数字，默认的输出输入进制都是十进制。数字有2个属性 长度(length)和小数点后精度(scale), length值数字有效数字的长度，scale是值小数点后的长度。
    如:0.001 length=3 scale=3
    45.78 length=4 scale=2
　　关于数字，当使用十六进制时，英文ABCDEF必须大写，大于16进制的则都用XX的十进制数字代表一位，如C=12  
### bc + 文件名
    bc "calc.txt"   进入bc交互式界面并自动返回文本内算式的结果  
    当算术或者语法等出现错误时，程序会返回错误信息，如下:  
    1/0  
    Runtime error (func=(main), adr=3): Divide by zero  
