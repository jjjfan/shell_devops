# shell习题解析91_95.md
---  

## 【技巧】  
### expect脚本的嵌套，结尾需要EOF顶头
### 死循环判断是否输入为空
        while true
        do
            read -p "请输入你要执行的操作：(stop/start/rm) " opt
            if [ -z "$opt" ]
            then
                echo "请输入要执行的操作。"
                continue
            else
                break
            fi
        done  
### 判断字串是否以指定字符'/'开头 
        if echo $1 |grep -q '^/.*'
        then
            echo "字串是以/开头的绝对路径。"
        fi   
### 查询指定包是否安装，没有安装就开始安装，通过命令返回 #? 值不为0判断安装是否成功
        if ! rpm -q samba >/dev/null
        then
            echo "将要安装samba"
            sleep 1
            yum install -y samba
            if [ $? -ne 0 ]
            then
                echo "samba安装失败"
                exit 1
            fi
        fi 
###  eval可读取一连串的参数，然后再依参数本身的特性来执行。
        ubaugust@DESKTOP-QQI3DMT:~$ a="11"
        ubaugust@DESKTOP-QQI3DMT:~$ echo '${'"a"'}'
        ${a}
        ubaugust@DESKTOP-QQI3DMT:~$ eval echo '${'"a"'}'
        11
### 判断参数个数，并给出相应的应用提示
        if [ $# -ne 2 ]
        then
            echo "Useage $0 盘符 挂载点, 如： $0 /dev/xvdb /data"
            exit 1
        fi        
   

