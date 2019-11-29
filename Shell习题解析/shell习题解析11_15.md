# shell习题解析11_15.md
---  
## seq命令.md
[seq命令.md](seq命令.md)  
## mkpasswd命令.md
[mkpasswd命令.md](mkpasswd命令.md)  
## iptables命令.md
[iptables命令.md](iptables命令.md)  




## 【技巧】  
### passwd --stdin 【用户名】   可以显示设置的密码，并且不需要验证，通常用于shell中脚本设置密码  
echo "aaaa" |passwd --stdin user1   设置用户user1的密码
echo -e "aaaa\naaaa" |passwd user1  设置用户user1的密码(新的密码：重新输入新的密码)
### echo -e选项，可以把\n作为换行符，处理特殊字符  
```  
        #echo -e "1\n2\n3"
        1
        2
        3
```
### echo -e选项，可以忽略换行符  
```  
        $echo -n "123"
        $echo "456"  
        最终输出 
        123456
```  
### 检查httpd进程数
pgrep -l httpd |wc -l
或是
ps -C httpd --no-heading |wc -l   
### 进程启动成功 echo $?的值是0
### 一分钟内的IP请求量高于100次，属于异常，需要拒绝掉

### 半小时内IP请求量，在pkts的数量（数据包）小于10次，说明恢复正常 
iptables -nvL
#### 把iptables的计数器清零 iptables -Z  

