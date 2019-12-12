# shell习题解析67_72.md
---  

## 【技巧】  
### 查看CPU的空闲百分比值
    top -bn1 |grep 'Cpu(s):'|sed 's/^%//'|awk -F ' +|%' '{print $8}'  
    在Centos6和Centos7上显示的不一样，区别在于空格或者%  
### 命令ps -elf 输出的PPID列为父进程的PID  
    pstree -p pid 同样可以得到   
    在安装psmisc包后有pstree命令  
      yum -y install psmisc  
### 使用(Here Documents)嵌入文档的形式(需顶格）  

        $mysqlc <<EOF
        create database $pro;  
        grant all on $pro.* to "$pro"@'127.0.0.1' identified by "$mysql_p";  
        #下面这个EOF必须要顶格  
        EOF
           
### 用嵌入文档（需顶格），把虚拟主机配置写入到配置文件里     
            
        cat >> $httpd_config_f <<EOF
        <VirtualHost *:80>
            DocumentRoot $webdir/$dom
            ServerName $dom
            <Directory $webdir/$dom>
                AllowOverride none
                Require all granted  
            </Directory>
        </VirtualHost>
        EOF
### 判断参数个数  
 
        if [ $# -ne 3 ]
        then
            echo "你给的参数个数不对，应该给3个参数."
            exit
        fi
 
### 判断参数是否为数字  
方式一  

        if_number()  
        {  
            n1=`echo $1|sed 's/[0-9.]//g'`  
            if [ -n "$n1" ]  
            then  
            echo "$1不是数字."  
            exit  
            fi  

            if echo $1|grep -q '^\.'   
            then  
            echo "数字$1不合法."  
                exit  
            fi  
        }  

方式二  

        if_number()  
        {  
            n=`echo $1|sed 's/[0-9.]//g'`  
            n2=`echo $1|sed 's/[^.]//g|wc -L'`  
            if [ -n "$n" ] || [ $n2 -gt 1]  
            then  
                echo "$1数字不合法（注意，不能是负数）."  
            exit 1  
            fi  
        }      

### 不打印换行符号 echo -n "■ "  不带-n参数的echo 打印换行符号  