# find与xargs的组合.md
---  
## 什么是xargs：  
	x 是加减乘除的乘号，args 则是 arguments (参数) 的意思，所以说，就是在产生某个指令的参数的意思；
	会使用 xargs 的原因是， 很多指令其实并不支持管线命令，因此我们可以透过 xargs 来提供该指令引用 standard input 之用。

## 实例：  
	1、搜索具体文件：在当前目录下，所有普通文件中搜索“hh”这个词
	find ./  -type f | xargs grep "hh"  
	2、与删除连用：
	①在当前目录下，删除1天以内的所有东西
	find ./ -mtime -1 | xargs rm -rf
	②在当前目录下，删除文件大小为0的文件
	find ./ -size 0 | xargs rm -rf
	3、搜索指定目录下的.txt文件，并依次修改文件名  
	find /123/ -type f -name "*.txt" | xargs -i mv {} {}.bak  
## find命令详解外链
[find命令详解](https://blog.csdn.net/m1585761297/article/details/80175634)  
[find命令学习](https://www.jianshu.com/p/44cc3bdd80e2)
