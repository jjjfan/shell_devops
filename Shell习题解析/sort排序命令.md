# sort排序命令.md
---  
## 按照指定的顺序升序排列  
        sort -t ":" -k 2n,2 file.log
## 按照指定的顺序降序进行排列  
        sort -t ":" -k 4rn,4 file.log
## 结果说明：
    1.-t 指定文本分隔符
    2.-k 指定排序列
    3.-n 按数字进行排序
    4.-r 翻转排序结果
## 其它参数  
参数：
    -b 忽略每行前面开始出的空格字符。
    -c 检查文件是否已经按照顺序排序。
    -f 排序时，忽略大小写字母。
    -M 将前面3个字母依照月份的缩写进行排序。
    -n 依照数值的大小排序。
    -o<输出文件> 将排序后的结果存入指定的文件。
    -r 以相反的顺序来排序。
    -t<分隔字符> 指定排序时所用的栏位分隔字符。
    -k 选择以哪个区间进行排序。
## 指定排序第几列  
    ip.txt 里存储着ip信息 统计排序后取前10条
    awk ‘{cnt[$1]++} END{for (ip in cnt) print ip":"cnt[ip]}‘ ip.txt | sort -k 2 -rn -t":" | head -n 10
    awk ‘{cnt[$1]++} END{for (ip in cnt) print cnt[ip],ip}‘ ip.txt | sort -rn | head -n 10
    sort -k  根据第几列排序  -n 按数字排序  -r 倒序 -t 分隔符
### 代码示例:
```  
        最终的linux命令如下：
        sort -t $'\t' -k 1n,1 -k 2n,2 -k4rn,4 -k3,3 my-file
        解释如下：
        -t $'\t'：指定TAB为分隔符
        -k 1, 1: 按照第一列的值进行排序，如果只有一个1的话，相当于告诉sort从第一列开始直接到行尾排列
        n:代表是数字顺序，默认情况下市字典序，如10<2
        r: reverse 逆序排列，默认情况下市正序排列
```  

### sort命令详解外链
https://www.cnblogs.com/itxiongwei/p/8528838.html
