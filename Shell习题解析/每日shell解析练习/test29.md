# 考试29.md  
---  
## 考试29  
1、写一个shell脚本，可以收集本机硬件信息：包括CPU（厂商型号、核数、）、内存（大小）、磁盘（名称和大小以及分区信息）、网卡（名称和IP）。  

## 【解答】   
```bash  
#!/bin/bash

cpu_cores=` grep 'cores' /proc/cpuinfo |uniq -c|awk -F': ' '{print $2}'`
echo "cpu_cores = $cpu_cores"
cpu_vendor=`grep '^vendor_id' /proc/cpuinfo |head -1|awk -F ': ' '{print $2}'`
echo "cpu_vendor = $cpu_vendor"

cpu_model=`grep '^model name' /proc/cpuinfo |head -1|awk -F ': +' '{print $2}'`
echo "cpu_model = $cpu_model"

memTotal=`grep '^MemTotal' /proc/meminfo |awk -F ': +' '{print $2}'`
echo "memTotal = $memTotal"
memFree=`grep '^MemFree' /proc/meminfo |awk -F ': +' '{print $2}'`
echo "memFree = $memFree"

for eth in `ip add |awk -F ': ' '$1 ~ "^[1-9]" {print $2}'|xargs`
do
        echo -n "$eth IPv4 add = "
        ip add show dev $eth |grep 'inet '|awk -F'inet |/' '{print $2}'

done

``` 

### 【答案】 
```bash  



```  

