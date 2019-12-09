# shell习题解析51_55.md
---  

## 【技巧】  
### curl -I 命令加上管道后，会有下载百分比、速度等信息
```bash  
ubaugust@DESKTOP-QQI3DMT:~$ curl -l www.apelearn.com/index.php|head 1
head: cannot open '1' for reading: No such file or directory
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
curl: (23) Failed writing body (0 != 8013)
ubaugust@DESKTOP-QQI3DMT:~$
ubaugust@DESKTOP-QQI3DMT:~$ curl -I www.apelearn.com/index.php 2>/dev/null
HTTP/1.1 200 OK
Server: nginx
Date: Mon, 09 Dec 2019 11:26:15 GMT
Content-Type: text/html; charset=UTF-8
Connection: keep-alive
Vary: Accept-Encoding
X-Powered-By: PHP/5.6.10

ubaugust@DESKTOP-QQI3DMT:~$
ubaugust@DESKTOP-QQI3DMT:~$ curl -I www.apelearn.com/index.php  |head -1
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
HTTP/1.1 200 OK
ubaugust@DESKTOP-QQI3DMT:~$ curl -I www.apelearn.com/index.php 2>/dev/null |head -1
HTTP/1.1 200 OK
ubaugust@DESKTOP-QQI3DMT:~$

```   

### 查找小于5k的文件 find ./ -type f -size -5k  
### 匹配时间10点到12点正则表达式 “09/Dec/2019:1[01]:[0-5][0-9]:”   
    命令为 `date +%d/%b/%Y:1[01]:[0-5][0-9]:`  