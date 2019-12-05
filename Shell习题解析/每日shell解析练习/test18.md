# 考试18.md  
---  
## 考试18  
1、写一个shell脚本，为mysql中aming用户增加一个授权IP123.45.67.89。</p><p>假设：已知mysql root用户密码为root_passwd123，目前aming用户只有一个授权ip。
提示：
select host from mysql.user where user=aming;  
show grants for aming@ip;  

## 【解答】   
```bash  

#!/bin/bash
ip="123.45.67.89"
Mysql_c="mysql -uroot -proot_password123"
$Mysql_c -e "grant all on *.* to 'aming'@'$ip' "  

```  
