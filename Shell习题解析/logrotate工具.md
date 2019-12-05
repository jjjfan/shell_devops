# logrotate工具.md  
---  
## 介绍
　　logrotate旨在简化生成大量日志文件的系统的管理。它允许日志文件的自动轮换、压缩、删除和邮件。每个日志文件可以每天、每周、每月处理，也可以在它变得太大时处理。通常，logrotate作为每日cron作业运行。它不会在一天内多次修改日志，除非日志的标准是基于日志的大小，并且logrotate每天运行多次，或者使用-f或--force选项。命令行上可以给出任意数量的配置文件。稍后的配置文件可能会覆盖前面文件中给出的选项，因此列出logrotate配置文件的顺序很重要。通常，应该使用一个配置文件，其中包含所需的任何其他配置文件。有关如何使用include指令来实现此目的的更多信息，请参见下面的内容。如果命令行上给出了一个目录，则该目录中的每个文件都用作配置文件。如果没有给出命令行参数，logrotate将打印版本和版权信息，以及简短的使用摘要。如果在轮换日志时发生错误，logrotate将以非零状态退出。  
### 其特点：  
通过让用户来配置规则的方式，检测和处理日志文件。配合Cron可让处理定时化；
预制了大量判断条件和处理方式，可大大降低手写脚本的负担和出错的可能；
Logrorate检测日志文件属性，比对用户配置好的检测条件，对满足条件的再根据用户配置的要求来处理，整个可以通过Cron来定时调度。
## 组成  
        /usr/bin/logrotate 程序所在位置；
        /etc/cron.daily/logrotate 默认让Cron每天执行logrotate一次；
        /etc/logrotate.conf 全局配置文件；
        /etc/logrotate.d 应用自个的配置文件存放目录，覆盖全局配置；
## logrotate命令格式：  
logrotate [OPTION...] <configfile>
        -d, --debug ：debug模式，测试配置文件是否有错误。
        -f, --force ：强制转储文件。
        -m, --mail=command ：压缩日志后，发送日志到指定邮箱。
        -s, --state=statefile ：使用指定的状态文件。
        -v, --verbose ：显示转储过程。
## 参数说明  
compress 通过gzip 压缩转储以后的日志  
nocompress 不做gzip压缩处理  
copytruncate 用于还在打开中的日志文件，把当前日志备份并截断；是先拷贝再清空的方式，拷贝和清空之间有一个时间差，可能会丢失部分日志数据。  
nocopytruncate 备份日志文件不过不截断  
create mode owner group 轮转时指定创建新文件的属性，如create 0777 nobody nobody  
nocreate 不建立新的日志文件  
delaycompress 和compress 一起使用时，转储的日志文件到下一次转储时才压缩  
nodelaycompress 覆盖 delaycompress 选项，转储同时压缩。  
missingok 如果日志丢失，不报错继续滚动下一个日志  
errors address 专储时的错误信息发送到指定的Email 地址  
ifempty 即使日志文件为空文件也做轮转，这个是logrotate的缺省选项。  
notifempty 当日志文件为空时，不进行轮转  
mail address 把转储的日志文件发送到指定的E-mail 地址  
nomail 转储时不发送日志文件  
olddir directory 转储后的日志文件放入指定的目录，必须和当前日志文件在同一个文件系统  
noolddir 转储后的日志文件和当前日志文件放在同一个目录下  
sharedscripts 运行postrotate脚本，作用是在所有日志都轮转后统一执行一次脚本。如果没有配置这个，那么每个日志轮转后都会执行一次脚本  
prerotate 在logrotate转储之前需要执行的指令，例如修改文件的属性等动作；必须独立成行  
postrotate 在logrotate转储之后需要执行的指令，例如重新启动 (kill -HUP) 某个服务！必须独立成行  
daily 指定转储周期为每天  
weekly 指定转储周期为每周  
monthly 指定转储周期为每月  
rotate count 指定日志文件删除之前转储的次数，0 指没有备份，5 指保留5 个备份  
dateext 使用当期日期作为命名格式  
dateformat .%s 配合dateext使用，紧跟在下一行出现，定义文件切割后的文件名，必须配合dateext使用，只支持 %Y %m %d %s 这四个参数  
size(或minsize) log-size 当日志文件到达指定的大小时才转储，log-size能指定bytes(缺省)及KB (sizek)或MB(sizem).当日志文件 >= log-size 的时候就转储。  

#### 以下是对test.log进行的切割：
在/etc/logrotate.d/下创建test配置文件：
```  
# cat test 
        /datadisk/data/log/test/test.log {
                rotate 5
                missingok
                create 644 root root
                compress
                delaycompress
        }
```  
在执行了5次logrotate -f /etc/logrotate.d/test之后可以看到日志文件 

#### 关于rotate轮换简单的理解就是：  
第一次执行完rotate(轮转)之后，原本的test会变成test.1，而且会制造一个空的test给系统来储存日志；
第二次执行之后，test.1会变成test.2，而test会变成test.1，又造成一个空的test来储存日志;
如果仅设定保留五个日志（即轮转5次）的话，那么执行第五次时，则 test.5这个档案就会被删除，保存最新的几个日志，compress会压缩转储后面的日志。
#### 对nginx日志进行切割：  
```  
        /datadisk/data/log/nginx/access.log {
                daily
                rotate 5
                missingok
                notifempty
                dateext
                compress
                delaycompress
                sharedscripts
                postrotate
                    if [ -f /var/run/nginx.pid ];then
                        kill -USR1 `cat /var/run/nginx.pid`
                    fi
                endscript
        }
```  
        Nginx是通过postrotate指令发送USR1信号来通知Nginx重新打开日志文件的。但是其他的应用程序不一定遵循这样的约定，比如说MySQL是通过flush-logs来重新打开日志文件的，可以在/etc/logrotate.d/目录下查看默认的mysql的配置。更有甚者，有些应用程序就压根没有提供类似的方法，此时如果想重新打开日志文件，就必须重启服务，但为了高可用性，这往往不能接受。还好Logrotate提供了一个名为copytruncate的指令，此方法采用的是先拷贝再清空的方式。

