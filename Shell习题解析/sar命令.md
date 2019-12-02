# sar命令.md
---  
    sar（System Activity Reporter系统活动情况报告）是目前 Linux 上最为全面的系统性能分析工具之一，可以从多方面对系统的活动进行报告，包括：文件的读写情况、系统调用的使用情况、磁盘I/O、CPU效率、内存使用状况、进程活动及IPC有关的活动等。本文主要以CentOS 6.3 x64系统为例，介绍sar命令。  
    yum install -y sysstat  安装

## sar命令常用格式  
sar [options] [-A] [-o file] t [n]  
###其中：  
    t为采样间隔，n为采样次数，默认值是1；  
    -o file表示将命令结果以二进制格式存放在文件中，file 是文件名。  
    options 为命令行选项，sar命令常用选项如下：   
            -A：所有报告的总和  
            -u：输出CPU使用情况的统计信息  
            -v：输出inode、文件和其他内核表的统计信息  
            -d：输出每一个块设备的活动信息  
            -r：输出内存和交换空间的统计信息  
            -b：显示I/O和传送速率的统计信息  
            -a：文件读写情况  
            -c：输出进程统计信息，每秒创建的进程数  
            -R：输出内存页面的统计信息  
            -y：终端设备活动情况  
            -w：输出系统交换活动信息  

## 1. CPU利用率
sar -p （查看全天）  
sar -u 1 10 （1：每隔一秒，10：写入10次）  
### 1.1. CPU输出项说明
| 输出项     | 详细说明                                          |
|---------|-----------------------------------------------|
| CPU     | all 表示统计信息为所有 CPU 的平均值。                       |
| %user   | 显示在用户级别\(application\)运行使用 CPU 总时间的百分比。       |
| %nice   | 显示在用户级别，用于nice操作，所占用 CPU 总时间的百分比。             |
| %system | 在核心级别\(kernel\)运行所使用 CPU 总时间的百分比。             |
| %iowait | 显示用于等待I/O操作占用 CPU 总时间的百分比。                    |
| %steal  | 管理程序\(hypervisor\)为另一个虚拟进程提供服务而等待虚拟 CPU 的百分比。 |
| %idle   | 显示 CPU 空闲时间占用 CPU 总时间的百分比。                    |

## 2. 内存利用率  
sar -r （查看全天）  
sar -r 1 10 （1：每隔一秒，10：写入10次）  
### 2.1. 内存输出项说明
| 输出项                | 详细说明                                          |
|--------------------|-----------------------------------------------|
| kbmemfree          | 这个值和free命令中的free值基本一致，所以它不包括buffer和cache的空间。 |
| kbmemused          | 这个值和free命令中的used值基本一致，所以它包括buffer和cache的空间。   |
| %memused           | 这个值是kbmemused和内存总量\(不包括swap\)的一个百分比。          |
| kbbuffers和kbcached | 这两个值就是free命令中的buffer和cache。                   |
| kbcommit           | 保证当前系统所需要的内存，即为了确保不溢出而需要的内存\(RAM\+swap\)。     |
| %commit            | 这个值是kbcommit与内存总量\(包括swap\)的一个百分比。            |

## 3. 磁盘I/O  
sar -d （查看全天）  
sar -d 1 2 （1：每隔一秒，2：写入2次）  
### 3.1. IO输出项说明  
| 输出项   | 详细说明                        |
|-------|-----------------------------|
| await | 表示平均每次设备I/O操作的等待时间（以毫秒为单位）。 |
| svctm | 表示平均每次设备I/O操作的服务时间（以毫秒为单位）。 |
| %util | 表示一秒中有百分之几的时间用于I/O操作。       |

## 4. 网络流量  
sar -n DEV （查看全天）  
sar -n DEV 1 2 （1：每隔一秒，2：写入2次）  
### 4.1. DEV输出项说明  
| 输出项      | 详细说明            |
|----------|-----------------|
| IFACE    | 就是网络设备的名称。      |
| rxpck/s  | 每秒钟接收到的包数目。     |
| txpck/s  | 每秒钟发送出去的包数目。    |
| rxkB/s   | 每秒钟接收到的字节数。     |
| txkB/s   | 每秒钟发送出去的字节数。    |
| rxcmp/s  | 每秒钟接收到的压缩包数目。   |
| txcmp/s  | 每秒钟发送出去的压缩包数目。  |
| rxmcst/s | 每秒钟接收到的多播包的包数目。 |


## 【外链】  
sar命令详解  
[http://lovesoo.org/linux-sar-command-detailed.html?esjqjk=6m2om2](http://lovesoo.org/linux-sar-command-detailed.html?esjqjk=6m2om2)


