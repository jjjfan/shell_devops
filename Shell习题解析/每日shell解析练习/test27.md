# 考试27.md  
---  
## 考试27  
    1、假设你妈妈的生日是阳历8月10日，写一个shell脚本，在你妈妈过生日前的1周，每天早晨8点都要发一封提醒邮件给你，一直提醒到8月8日那天，要求脚本写完后放入任务计划每天8点执行。   

## 【解答】  
```bash   
#!/bin/bash

curYear=`date +%Y`
birMD="0810"
tarMD="0808"
birthDay=$curYear$birMD
#echo "birthDay is $birthDay"
#startWarningDay=`date -d "$birthDay 1  week ago" +%Y%m%d`
startWarningDay=`date -d "$birthDay 1  week ago" +%s`
#echo "startWarningDay is $startWarningDay"
#endWarningDay=$curYear$tarMD
endWarningDay=`date -d "$curYear$tarMD" +%s`
#echo "end W day is $endWarningDay"

nowDay=`date +%s`
if [ $nowDay -le $endWarningDay  ] && [ $nowDay -ge $startWarningDay  ]
then
        python /usr/local/sbin/mail.py $ma "生日 $birthDay  的提醒" "生日提醒 $birthDay"
fi

```  


### 【答案】 
```bash  



```  

