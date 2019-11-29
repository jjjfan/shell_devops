# seq命令.md  
---  
## seq 用于生成从一个数到另一个数之间的所有整数。
		#seq 1 5  生成数字1到5
		1
		2
		3
		4
		5
## 用法：seq [选项]... 尾数
	　或：seq [选项]... 首数 尾数
	　或：seq [选项]... 首数 增量 尾数
## 选项：

     -f, --format=FORMAT      use printf style floating-point FORMAT
     -s, --separator=STRING   use STRING to separate numbers (default: \n)
     -w, --equal-width        equalize width by padding with leading zeroes
## -f 指定输出格式
	#seq -f “%3g” 13  数字位数为三位，不足补空格
	  1
	  2
	  3
	#seq -f “%03g” 1 5  数字位数为三位，不足补零
	001
	002
	003
	004
	005
	#seq -f "str%03g" 1 3
	str001
	str002
	str003
    #seq 1 2 9 从1到9，指定增值为2  
    1
    3
    5
    7
    9
# -w 指定输出数字同宽，与-f部分作用相似，不可与-f选项同时使用  
	#seq -w  8 12
	08
	09
	10
	11
	12
# -s 指定分隔符，默认分隔符是/n（回车）  
	#seq -s  " " 1 5  空格作为分隔符
	1 2 3 4 5 

	#seq -s "`echo -e "\t"`" 1 3  \t作为分隔符
	1  2    3

