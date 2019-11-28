# shell习题解析06_10.md
---  
## sed命令.md
[sed命令.md](sed命令.md)  
## sort排序命令.md
[sort排序命令.md](sort排序命令.md)  
## 查看CPU和内存信息.md
[查看CPU和内存信息.md](查看CPU和内存信息.md)  
## find命令之exec.md
[find命令之exec.md](find命令之exec.md) 

## 【技巧】  
### 检测服务是否运行，可以判断端口是否开启
httpd  80 
#### netstat -lntp |grep -q ':80 '   
80后面有空格，目的是为了精确匹配，排除类似8080端口   
#### pgrep  -l httpd  
列出所有的 httpd 进程的pid  
#### pgrep  -l sshd  
列出所有的 sshd 进程的pid  
#### date +%w  
获取一周中的第几天  
#### date +%d  
获取一月中的几日  
#### date +"%F %T"  
获取日期和时间样式：
2019-11-28 20:25:41  
### 检测502状态码  
在日志/data/log/access.log中，10s内的日志条数在300左右，502状态码超过10%就是很严重了，即阈值可以设置为10  
#### grep -c ' 502" ' /tmp/log  
过滤502状态码，并计数  
### sleep 50  
延时50秒，保证前面的服务指令有足够的时间启动  
### sed '/[a-zA-Z]/d' filename  
删除含有字母的行  
### sed 's/[a-zA-Z]//g' filename  
删除字符串里面的字母  
