# shell习题解析73_78.md
---  

## 【技巧】  
### xargs -i 可以对文件逐一操作，用'{}'表示每一个文件  
### 脚本中写嵌入式脚本(使用 <<EOF 和 EOF)时候，'$'符号需要脱意用'\'
### 使用tar命令 打包在文件列表/tmp/old_log中的文件
        tar czf $d.tar.gz `cat /tmp/old_log|xargs`  
### 删除在文件列表/tmp/old_log中的文件
        cat /tmp/old_log|xargs rm -f 
### awk中使用 -v 选项定义临时变量
        awk -v w2=$w -F ':' '$1==w2 {print $2}' 3.txt   
    同样 使用"''" 里面单引号外面双引号 的形式调用shell变量，可以达到同样效果
        awk -F':' '$1=="'$id'" {print $2}'  3.txt  
