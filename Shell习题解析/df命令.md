# df命令.md
---  
## df命令  
df命令用于查看磁盘的分区，磁盘已使用的空间，剩余的空间
### 用法  
df [选项] [文件..]  
### 命令选项    
-a,--all　　　　　　　　　全部文件系统  
-h,--human-readable　　　以以合适的单位来显示信息  
-H,--si　　　　　　　　　与-h参数相同，但在计算时是以1000 Bytes为换算单位而非1024 Bytes  
-i,--inodes　　　　　　　显示inode的信息  
-k,--kilobytes　　　　　指定区块大小为1024字节  
-l,--local　　　　　　　只显示本地文件系统  
-m,--megabytes　　　　　指定区块大小为1048576字节  
-P,--portability　　　　使用POSIX的输出格式  
--sync　　　　　　　　　 在取得磁盘使用信息前，先执行async指令  
-t<TYPE>,--type=<TYPE>       仅显示指定文件系统类型的磁盘信息  
-T,--print-type　　　　　　　显示文件系统的类型  
-x<TYPE>,--exclude-type=<TYPE>    　　不要显示指定文件系统类型的磁盘信息  
--help　　　　　　　　　　显示帮助  
--version　　　　　　　　显示版本信息  
### 实例  
[fan@desktop01 ~]# df -h  
```  
文件系统                  容量   已用  可用  已用% 挂载点  
/dev/mapper/centos-root   10G  1.1G  9.0G   11%  /  
devtmpfs                 350M     0  350M    0%  /dev  
tmpfs                    362M     0  362M    0%  /dev/shm  
tmpfs                    362M  6.0M  356M    2%  /run  
tmpfs                    362M     0  362M    0%  /sys/fs/cgroup  
/dev/sda1               1014M  130M  885M   13%  /boot  
tmpfs                     73M     0   73M    0%  /run/user/0  
```  

## 相关命令的解释：    
        df -hl 查看磁盘剩余空间   
        df -h 查看每个根路径的分区大小  
        du -sh [目录名] 返回该目录的大小   
        du -sm [文件夹] 返回该文件夹总M数   
        du -h [目录名] 查看指定文件夹下的所有文件大小（包含子文件夹）  

