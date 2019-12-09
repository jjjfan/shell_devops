# 考试15.md  
---  
## 考试15  
1、文件stu.txt内容：
    100:张三:男:计算机
    101:张红:女:文秘
    102:张飞:男:体育
    103:张婷:女:英语
    104:张海洋:男:机电

该文件是所有学生的信息，每个学生存储一行信息，信息格式如下：学号:姓名:性别:专业 如(100:张三:男:计算机)设计一个shell，名称为stu.sh,该shell完成如下功能:
1)当输入stu.sh时，列出所有记录内容
2)当输入 stu.sh -a 100:张三:男:计算机时，首先判断100记录是否存在，如果不存在，则把该信息写入文件，如果存在，则给出提示，并输出文件中学号为100的该行信息
3)当输入 stu.sh -d 100时，首先判断100记录是否存在，如果不存在，给出提示，如果存在，则提示用户确认是否要删除记录，如用户输入y或者yes，则删除文件中学号为100的该行信息，如果用户输入n或no时，则不做删除操作
4)当输入 stu.sh -s 100时，首先判断100记录是否存在，如果不存在，给出提示，如果存在，则输出文件中学号为100的该行信息
5)当用户输入的选项不正确时，给出错误提示，并输入该shell的用法


## 【解答】   
```bash

#!/bin/bash
tag=0
num=

if [ $# -eq 2 ]
then
        num=`echo $2 |awk -F':' '{print $1}' |sed  's/[0-9]//g'`
        s=`echo $2 |awk -F':' '{print NF}'`
        if [ -n "$num" ]
        then
                tag=-1
                echo "stu num  $num not num "
        elif [ "$1" = "-a" ] && [ "$s" -eq 4  ];
        then
                tag=2
                num=`echo $2 |awk -F':' '{print $1}'|sed 's/[^0-9]//g'`
        elif [ $1 = "-d" ]
        then
                tag=3
                num=`echo $2 |awk -F':' '{print $1}'|sed 's/[^0-9]//g'`
        elif [ $1 = "-s"  ]
        then
                tag=4
                num=`echo $2 |awk -F':' '{print $1}'|sed 's/[^0-9]//g'`
        fi
elif [ $# -eq 0 ]
then
        tag=1
fi

case $tag in
        1)
                echo "stuNO    name    sex    course"
                awk -F':' '{OFS="     "} {print $1,$2,$3,$4} '  stu.txt
                ;;
        2)
                cmd=`awk -F':'  '{if ($1=="'$num'")  {print NR}} ' stu.txt |sed 's/[^0-9]//g'`
                if [ -z $cmd ]
                then
                        cmd=0
                fi


                if [ -n $cmd ] && [ $cmd -gt 0 ]
                then
                        echo "stdNO $num existing!!!"
                        awk -F':' '{if ($1=="'$num'")  {print $1,$2,$3,$4}} ' stu.txt
                else
                        echo "$2" >> stu.txt
                        echo "in -a $num to add $2"
                fi
                #awk -F':' '{if ($1=="'$num'")  {print $1,$2,$3,$4}} ' stu.txt

                ;;
        3)
                echo "in 3 done -d 100 to delete"
                cmd=`awk -F':'  '{if ($1=="'$num'")  {print NR}} ' stu.txt |sed 's/[^0-9]//g'`
                #echo $cmd
                if [ -z $cmd ]
                then
                        cmd=0
                fi

                if [ -n $cmd ] && [ $cmd -gt 0 ]
                then
                        echo "stdNO $num existing!!!"
                        read -p "Please yes or no delete line(y/n):" n
                        if [ -z $n  ]
                        then
                                n="n"
                        elif [ $n = "yes"  ] || [ $n = "y"  ]
                        then
                                sed -i ''$cmd''d  stu.txt  #&&>/dev/null
                                echo "having delete stuNO $num line!!!"
                        fi
                else
                        echo "in -d $num to not exist!!!"
                fi
                ;;
        4)
                echo "in 4 done -s 100 to show one"
                cmd=`awk -F':'  '{if ($1=="'$num'")  {print NR}} ' stu.txt |sed 's/[^0-9]//g'`
                #echo $cmd
                if [ -z $cmd ]
                then
                        cmd=0
                fi

                if [ -n $cmd ] && [ $cmd -gt 0 ]
                then
                        echo "stdNO $num existing!!!"
                        awk -F':' '{if ($1=="'$num'")  {print $1,$2,$3,$4}} ' stu.txt

                else
                        echo "in -s $num to not exist!!!"
                fi
                ;;
        0)
                echo "error info !!!"
                ;;
        *)
                echo "stu num error"
                echo "error info"

esac


echo "===== end ====="

``` 

### 【答案】 
```bash  
        #!/bin/bash
        data="stu.txt";
        sid="学号";
        sname="姓名";
        ssex="性别";
        smajor="专业";

        help(){
          echo "不加参数，显示所有记录";
          echo "-a 添加记录";
          echo "-d 删除记录";
          echo "-s 搜索记录";
        }

        if [ $# -eq 0  ];
        then
          printf "%-s\t%-s\t%-s\t%-s\n" $sid $sname $ssex $smajor;
          #cat $data |awk -F ":" '{printf("%-s\t%-s\t%-s\t%-s\n",$1,$2,$3,$4);}';二选一
          cat $data|tr ':' '\t';
          exit;
        fi

        case $1 in 
        -a)
          if ! grep -q $2 $data 2>&1;
          then
                echo $2>>$data;
                exit;
          else
                echo "存在";
                printf "%-s\t%-s\t%-s\t%-s\n" $sid $sname $ssex $smajor;
                echo $2|tr ':' '\t';
          fi
        ;;
        -d)
          if ! grep -q $2 $data 2>&1;
          then
                echo "记录不存在。。";
                exit;
          else
                read -p "确定要删除？(y/n)" confirm;
                if [ $confirm == "y" -o $confirm == "yes" ];
                then
                        sed -i "/$2/d" $data 2>&1;
                elif [ $confirm == "n" -o $confirm == "no" ];
                then
                        echo "用户取消";
                else
                        echo "错误的输入";
                fi
          fi
        ;;
        -s)
          if ! grep -q $2 $data 2>&1;
          then
                echo "记录不存在。。";
                exit;
          else
                printf "%-s\t%-s\t%-s\t%-s\n" $sid $sname $ssex $smajor;
                #sed -n "/$2/p" $data |tr ':' '\t';
                grep $2 $data|tr ':' '\t';
          fi
        ;;
        *)
          help
        ;;
        esac

```  

