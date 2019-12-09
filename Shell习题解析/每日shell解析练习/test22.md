# 考试22.md  
---  
## 考试22  
    1、某业务由web1、web2、web3共3台机器在提供服务，写一个shell脚本，检测这3台机器哪一台请求异常。假如测试链接为http://www.example.com/test.php，超过3秒未得到请求结果则判为异常，正常状态码为200   
    思路：  
    使用curl  --connect-timeout 3 -I  -x  检测  

## 【解答】   
```bash  

#!/bin/bash
checkcon()
{
url="https:// www.baidu.com/"
#url="http:// www.example.com/test.php"

flag=`curl --connect-timeout 3 -I -x $url 2>/dev/null| head -1|awk '{print $2}'`
if [ $flag != 200 ]
then
        echo "connect error timeout 3 !!!"
fi
#echo $flag
}

web1=
web2=
web3=
url="https:// www.baidu.com/"
#url="http:// www.example.com/test.php"

flag="curl --connect-timeout 3 -I -x $url 2>/dev/null| head -1|awk '{print $2}' "
sta=`ssh $web1 -e "$flag"`
if [ $flag != 200 ]
then
        echo "web1 connect error timeout 3 !!!"
fi

sta=`ssh $web2 -e "$flag"`
if [ $flag != 200 ]
then
        echo "web2 connect error timeout 3 !!!"
fi

sta=`ssh $web3 -e "$flag"`
if [ $flag != 200 ]
then
        echo "web3 connect error timeout 3 !!!"
fi


```  
### 【答案】 
```bash  



```  



