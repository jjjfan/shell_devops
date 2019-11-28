# 查看CPU和内存信息.md
---  
## 查看CPU规格  
cat /proc/cpuinfo |grep name |cut -f2 -d: |uniq -c 

## 查看内存信息  
cat /proc/meminfo

## 查看系统版本信息
cat /etc/issue
