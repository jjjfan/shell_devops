# mkpasswd命令.md  
---  
## mkpasswd命令 是make password的简写。可以随机生成字符串。
### 安装：
```
	# yum install -y expect
```  


### 语法：  mkpasswd [选项] [参数]
### 选项：  
		-l：指定长度
		-d：数字的个数
		-c：小写字母个数
		-C：大写字母个数
		-s：特殊字符个数

## 实例
### 生成一个15位的密码，特殊符号0个，数字5个
```  
	# mkpasswd -l 15 -s 0 -d 5
	zv63Zw2Uj8mp1cy
```  
### mkpasswd 默认生成9位随机密码
### mkpasswd -l 12  生成12位的随机密码
### mkpasswd -s 3  密码中包含3位特殊符号