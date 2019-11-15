# find命令使用.md
---  
# find -exec 命令后面的\;和+  

一个-exec只能执行一个命令，而且必须在命令后面加上终结符，终结符有两个：“；”和“+”。
其中“；”会对每一个find到的文件去执行一次cmd命令。而”+“让find到的文件一次性执行完cmd命令。

### 为什么必须有终结符？
因为一个find后面可以有多个-exec cmd，所以必须要有终结符分割他们。如果不加，会包缺少参数。
```
[root@VM_16_6_centos ~]# find / -maxdepth 2 -type f -name "*.log" -exec echo {} \;
/tmp/setRps.log
/tmp/net_affinity.log
/tmp/nv_gpu_conf.log
[root@VM_16_6_centos ~]# find / -maxdepth 2 -type f -name "*.log" -exec echo {} +
/tmp/setRps.log /tmp/net_affinity.log /tmp/nv_gpu_conf.log
[root@VM_16_6_centos ~]#
```
#### 一个find后面多个-exec cmd  如下：  
```
[root@VM_16_6_centos ~]# find / -maxdepth 2 -type f -name "*.log" -exec echo {} \; -exec echo {} +
/tmp/setRps.log
/tmp/net_affinity.log
/tmp/nv_gpu_conf.log
/tmp/setRps.log /tmp/net_affinity.log /tmp/nv_gpu_conf.log
[root@VM_16_6_centos ~]# 
```

### 为什么要加“\”?
“；”是shell的命令分隔符，如果只有“；”，那么这条命令就会被shell截断。  
```
[root@VM_16_6_centos ~]# find / -maxdepth 2 -type f -name "*.log" -exec echo {} ;
find: missing argument to `-exec'
[root@VM_16_6_centos ~]# find / -maxdepth 2 -type f -name "*.log" -exec echo {} \;
/tmp/setRps.log
/tmp/net_affinity.log
/tmp/nv_gpu_conf.log
[root@VM_16_6_centos ~]# 
```  

