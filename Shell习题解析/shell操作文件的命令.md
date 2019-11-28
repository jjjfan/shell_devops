# shell操作文件的命令.md  
---  
## 删除最后一列、删除第一行、diff等
    删除文件第一行： sed '1d' filename  
    删除文件最后一列： awk '{print $NF}' filename  
    awk删除重复行的命令：awk '{if (!seen[$0]++) {print $0;}}' filename  
## 比较文件的两种方法：  
    1）comm -3 --nocheck-order file1 file2  
    2) grep -v -f file1 file2 :输出file2中有file1中没有的行
    当然还有diff file1 file2  