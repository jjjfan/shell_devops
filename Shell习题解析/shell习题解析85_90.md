# shell习题解析85_90.md
---  

## 【技巧】  
### 取日志的最后1000条记录
    tail -1000 $log 
### 服务器上 1秒可以有上千条访问日志
### 在centos6系统 开机服务控制可以用chkconfig工具或是ntsysv命令
### 输出指定字体的颜色
    格式: echo -e "\033[字背景颜色;字体颜色m字符串\033[0m"   
    例如: 
        echo -e "\033[41;36m something here \033[0m"   
        其中41的位置代表底色, 36的位置是代表字的颜色   
            字背景颜色范围:40----49 
                40:黑 
                41:深红 
                42:绿 
                43:黄色 
                44:蓝色 
                45:紫色 
                46:深绿 
                47:白色 
            字颜色:30-----------39 
                30:黑 
                31:红 
                32:绿 
                33:黄 
                34:蓝色 
                35:紫色 
                36:深绿 
                37:白色 
### Psmisc软件包包含三个帮助管理/proc目录的程序(pstree、killall、 fuser、)
        centos下使用yum安装  
            yum install psmisc  
### 查询域名信息 whois www.aaa.com
        需要安装包 yum install -y jwhois 
        在脚本中判断是否有安装包
        which whois >/dev/null 2>/dev/null
        if [ $? -ne 0 ]
        then
            yum install -y epel-release
            yum install -y jwhois
        fi           
### 时间戳一天的值为86400
        计算7天的值 echo "86400*7|bc"  
### 判断包是否安装
        if ! rpm -q $1 &>/dev/null
        then
            yum installl -y $1
        fi        
### ssh-keygen常用参数
        -t：指定生成密钥的类型，默认使用SSH2d的rsa  
        -f：指定生成密钥的文件名，默认id_rsa（私钥id_rsa，公钥id_rsa.pub）  
        -P：提供旧密码，空表示不需要密码（-P ‘’）  
        -N：提供新密码，空表示不需要密码(-N ‘’)  
        -b：指定密钥长度（bits），RSA最小要求768位，默认是2048位；DSA密钥必须是1024位（FIPS 1862标准规定）  
        -C：提供一个新注释  
        -R hostname：从known_hosta（第一次连接时就会在家目录.ssh目录下生产该密钥文件）文件中删除所有属于hostname的密钥        
### 一些linux 系统中的中文文档
[金步国作品集 http://www.jinbuguo.com/](http://www.jinbuguo.com/)    
    Email(QQ)：70171448在QQ邮箱              
