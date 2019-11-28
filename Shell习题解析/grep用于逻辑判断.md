# grep用于逻辑判断.md
---  
## grep -q用于if逻辑判断       
        -q 参数，本意是 Quiet; do not write anything to standard output.  Exit immediately with zero status if any match is found, even if an error was detected.   中文意思为，安静模式，不打印任何标准输出。如果有匹配的内容则立即返回状态值0。  

        在shell脚本中，你只需要知道grep有没有找到指定的字符串，而不需要满屏幕打印出来，因为那样会很难看。这只可以加-q选项，执行结果是：如果找到了，会返回0，否则，返回1。然后你在接下来的语句中检查$?的值，就知道grep有没有找到需要的字符串了。
        举个例子，假设文件a.txt的内容为：”aaaa“
        那么你grep -iq "a"
        然后echo $?
        输出是0
        如果grep -iq "aaa"
        然后echo $?
        结果是1


```  
        if ［ 1 -ne 1 ］;then
        ...
        fi
```  

    -eq 是等于
    -ne 是不等于
    -le 小于等于
    -ge 大于等于
    -lt 小于
    -gt 大于

## 实例  
```  
        #!/bin/bash        
        if $(ps | grep -q "ps");then
        echo "find ps"
        else
            echo "not find ps"
        fi
```  
        如果变量count值不是数字，则赋值为21
```  
        if echo $count | grep -q '[^0-9]'
        then
                count=21
        fi
```  