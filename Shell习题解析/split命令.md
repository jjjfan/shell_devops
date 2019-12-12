# split命令.md  
---  
## split 的命令格式：  
	split [-b ][-C ][-][-l ][要切割的文件][输出文件名前缀][-a ]

## 最常用的选项，都在这里了：
	-b<字节>：指定按多少字节进行拆分，也可以指定 K、M、G、T 等单位。
	-<行数>或-l<行数>：指定每多少行要拆分成一个文件。
	输出文件名前缀：设置拆分后的文件的名称前缀，split 会自动在前缀后加上编号，默认从 aa 开始。
	-a<后缀长度>：默认的后缀长度是 2，也就是按 aa、ab、ac 这样的格式依次编号。  
### 先使用 dd 命令来生成一个 700MB 文件来作为我们的拆分对象：  
	dd if=/dev/zero bs=1024 count=700000 of=king_of_ring.avi
### 把文件以 400MB 作为一个拆分单位，来进行拆分。这里使用到了 split 的-b选项，来指定每个拆分文件的大小：  
 
    [root@roclinux ~]$ split -b 400M king_of_ring.avi  		   
    [root@roclinux ~]$ ls -l  
    total 1400008  
    -rw-r--r-- 1 root root 716800000 Apr 12 13:01 king_of_ring.avi  
    -rw-r--r-- 1 root root 419430400 Apr 12 13:04 xaa  
    -rw-r--r-- 1 root root 297369600 Apr 12 13:04 xab  

### 使用 cat 命令将拆分文件 xaa 和 xab 合并成一个文件，可以看出合并后的文件和源文件的大小是一致的：  
		cat xaa xab > king_of_ring_merge.avi  
### 在 Windows 下的话，我们要先运行 cmd，然后用 copy 命令来进行文件的合并：  
		copy /b xaa + xab king_of_ring.avi  
## 设置拆分文件的名称前缀  

    #我们指定了king_of_ring_part_前缀  
    [root@roclinux ~]$ split -b 400m king_of_ring.avi king_of_ring_part_  
       
    #可以看到, 文件名的可读性提高了很多  
    [root@roclinux ~]$ ls -l king*  
    -rw-r--r-- 1 root root 716800000 Feb 25 18:29 king_of_ring.avi  
    -rw-r--r-- 1 root root 419430400 Feb 25 19:24 king_of_ring_part_aa  
    -rw-r--r-- 1 root root 297369600 Feb 25 19:24 king_of_ring_part_ab  
 				
## 设置数字后缀  
如果大家看不惯以 aa、ab 这种字母作为文件后缀，我们还可以通过-d选项来指定数字形式的文件后缀：	  

    #使用了-d选项  
    [root@roclinux ~]$ split -b 400m -d king_of_ring.avi king_of_ring_part_    
       
    #后缀从原来的aa、ab变成了00、01  
    [root@roclinux ~]$ ls -l king*  
    -rw-r--r-- 1 root root 716800000 Feb 25 18:29 king_of_ring.avi  
    -rw-r--r-- 1 root root 419430400 Feb 25 19:24 king_of_ring_part_00  
    -rw-r--r-- 1 root root 297369600 Feb 25 19:24 king_of_ring_part_01    
 
## 按照行数进行拆分  
  
    #使用-N来指定拆分的行数,本例中为-10  
    [root@roclinux ~]$ split -d -10 /etc/passwd my_passwd_  
       
    #可以看到拆分成功  
    [root@roclinux ~]$ wc -l my_passwd_*  
      10 my_passwd_00  
      10 my_passwd_01  
       5 my_passwd_02  
      25 total    
 
## 合并后的校验  
需要注意的是，在通过网络来传输大文件，或者在设备之间复制大文件的时候，可能会出现传输前后数据不一致的情况。  
使用 split 来拆分大文件仅仅是故事的开始，操作完毕后化零为整、完璧归赵才是完美的结局。因此需要在合并文件后进行文件的完整性校验，推荐使用 md5sum 来计算和比对前后两个大文件的 md5 值。  
 
    #对原先的文件计算md5值  
    [root@roclinux ~]$ md5sum king_of_ring.avi  
    eacff27bf2db99c7301383b7d8c1c07c  king_of_ring.avi  
       
    #对合并后的文件计算md5值, 并与原值进行比较  
    [root@roclinux ~]$ md5sum king_of_ring_merge.avi  
    eacff27bf2db99c7301383b7d8c1c07c  king_of_ring_merge.avi  
 