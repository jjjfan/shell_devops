# shell习题解析01_05.md
---  
## date命令.md
[date命令.md](date命令.md)  
## df命令.md
[df命令.md](df命令.md)  
## Shell中的反引号_单引号_双引号.md
[Shell中的反引号_单引号_双引号.md](Shell中的反引号_单引号_双引号.md)  
## shell中的条件判断.md
[shell中的条件判断.md](shell中的条件判断.md) 
## find与xargs的组合.md
[find与xargs的组合.md](find与xargs的组合.md)  


## 【技巧】
##### ps aux   
打印所有进程的信息  
##### grep -v 'RSS'   
过滤出来不含有RSS的行  
##### sum=$[$sum+1]   
注意$[...] 取得值，并赋值给变量sum  
##### ping -c100 180.163.26.39  
对目标地址发送ping包100次,丢包率100%表示目标不存活，实际网络环境只要超过20%就会有很大的问题   
##### awk -F ':|#|.'   
指定分割符可以是“：”，也可以是“#”，也可以是“.”，多个分割符用竖线“|”来划分。
实例分割字串 'recevied, |%'  注意里面含有的空格

  
