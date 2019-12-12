# shell习题解析56_60.md
---  
## bc命令.md
[bc命令.md](bc命令.md)  

## 【技巧】  
### 在指定的文档后面增加内容 sed 中a 表示追加，5a表示在第5行下面增加
    sed -i "5a # This is a test file.\n# Test insert line into this file." p1.txt
### 压缩当前目录下的文件到指定的目录下压缩文件名  
    tar czf /root/bak/$d2_etc.tar.gz ./    
    tar czf  `date +%y%m%d`_etc.tar.gz /etc/  
### 把文本中所有的非字母的字符替换为空格
    sed 's/[^a-zA-Z]/ /g' a.txt    
### 实现每行一列  xargs -n1     
     sed 's/[^a-zA-Z]/ /g' a.txt| xargs -n1 
     等效于
     for w in `sed 's/[^a-zA-Z]/ /g' $1`
     do
         echo $w
     done   
### 增加随机性 取字符串长度 加 $RANDOM产生的随机数 得到一个随机数 除以一个整数取余
