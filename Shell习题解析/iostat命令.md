# iostat命令md  
---  
iostat用于输出CPU和磁盘I/O相关的统计信息
## iostat语法
	用法：iostat [ 选项 ] [ <时间间隔> [ <次数> ]]

## 常用选项说明：  
	-c：只显示系统CPU统计信息，即单独输出avg-cpu结果，不包括device结果  
	-d：单独输出Device结果，不包括cpu结果  
	-k/-m：输出结果以kB/mB为单位，而不是以扇区数为单位  
	-x:输出更详细的io设备统计信息  
	interval/count：每次输出间隔时间，count表示输出次数，不带count表示循环输出  
	说明：更多选项使用使用man iostat查看  

## 常用实例 
	1、iostat，结果为从系统开机到当前执行时刻的统计信息  
		输出含义：
	    avg-cpu: 总体cpu使用情况统计信息，对于多核cpu，这里为所有cpu的平均值。重点关注iowait值，表示CPU用于等待io请求的完成时间。

	    Device: 各磁盘设备的IO统计信息。各列含义如下：
			Device: 以sdX形式显示的设备名称
			tps: 每秒进程下发的IO读、写请求数量
			KB_read/s: 每秒从驱动器读入的数据量，单位为K。
			KB_wrtn/s: 每秒从驱动器写入的数据量，单位为K。
			KB_read: 读入数据总量，单位为K。
			KB_wrtn: 写入数据总量，单位为K。

	2、iostat -x -k -d 1 2。每隔1S输出磁盘IO的详细详细，总共采样2次。  
		以上各列的含义如下：
		rrqm/s: 每秒对该设备的读请求被合并次数，文件系统会对读取同块(block)的请求进行合并
		wrqm/s: 每秒对该设备的写请求被合并次数
		r/s: 每秒完成的读次数
		w/s: 每秒完成的写次数
		rkB/s: 每秒读数据量(kB为单位)
		wkB/s: 每秒写数据量(kB为单位)
		avgrq-sz:平均每次IO操作的数据量(扇区数为单位)
		avgqu-sz: 平均等待处理的IO请求队列长度
		await: 平均每次IO请求等待时间(包括等待时间和处理时间，毫秒为单位)
		svctm: 平均每次IO请求的处理时间(毫秒为单位)
		%util: 采用周期内用于IO操作的时间比率，即IO队列非空的时间比率  
## 重点关注参数
		1、iowait% 表示CPU等待IO时间占整个CPU周期的百分比，如果iowait值超过50%，或者明显大于%system、%user以及%idle，表示IO可能存在问题。  
		2、avgqu-sz 表示磁盘IO队列长度，即IO等待个数。  
		3、await 表示每次IO请求等待时间，包括等待时间和处理时间  
		4、svctm 表示每次IO请求处理的时间  
		5、%util 表示磁盘忙碌情况，一般该值超过80%表示该磁盘可能处于繁忙状态。		
## 疑惑：dm-0/1/2是什么？怎么来的？
		我们根据可以得知：
		dm-0、dm-1、dm-2的主设备号是253（是linux内核留给本地使用的设备号），次设备号分别是0、1、2，这类设备在/dev/mapper中
		cd /dev/mapper/ 
		ll
		看到dm-0、dm-1、dm-2的详细设备名后，知道这三个设备是属于centos逻辑卷组的lvm设备。  		
## 输出内容详解：  
	%user：CPU处在用户模式下的时间百分比  
	%nice：CPU处在带NICE值的用户模式下的时间百分比  
	%system：CPU处在系统模式下的时间百分比  
	%iowait：CPU等待输入输出完成时间的百分比  
	%steal：管理程序维护另一个虚拟处理器时，虚拟CPU的无意识等待时间百分比  
	%idle：CPU空闲时间百分比  
### 当然了，iostat命令的重点不是用来看CPU的，重点是用来监测磁盘性能的。
		Device：设备名称  
		rrqm/s：每秒合并到设备的读取请求数  
		wrqm/s：每秒合并到设备的写请求数  
		r/s：每秒向磁盘发起的读操作数  
		w/s：每秒向磁盘发起的写操作数  
		rkB/s：每秒读K字节数  
		wkB/s:每秒写K字节数  
		avgrq-sz：平均每次设备I/O操作的数据大小  
		avgqu-sz：平均I/O队列长度  
		await：平均每次设备I/O操作的等待时间 (毫秒)，一般地，系统I/O响应时间应该低于5ms，如果大于 10ms就比较大了  
		r_await：每个读操作平均所需的时间；不仅包括硬盘设备读操作的时间，还包括了在kernel队列中等待的时间  
		w_await：每个写操作平均所需的时间；不仅包括硬盘设备写操作的时间，还包括了在kernel队列中等待的时间  
		svctm：平均每次设备I/O操作的服务时间 (毫秒)（这个数据不可信！）  
		%util：一秒中有百分之多少的时间用于I/O操作，即被IO消耗的CPU百分比，一般地，如果该参数是100%表示设备已经接近满负荷运行了  		
## 性能监控指标
	上面说了这么多，也看了那么多的系统输出，那我们在日常运维中到底需要关注哪些字段呢？下面就来说说这篇文章的重点了，我们到底该关注哪些输出内容就可以确定这台服务器是否存在IO性能瓶颈。
		%iowait：如果该值较高，表示磁盘存在I/O瓶颈
		await：一般地，系统I/O响应时间应该低于5ms，如果大于10ms就比较大了
		avgqu-sz：如果I/O请求压力持续超出磁盘处理能力，该值将增加。如果单块磁盘的队列长度持续超过2，一般认为该磁盘存在I/O性能问题。需要注意的是，如果该磁盘为磁盘阵列虚拟的逻辑驱动器，需要再将该值除以组成这个逻辑驱动器的实际物理磁盘数目，以获得平均单块硬盘的I/O等待队列长度
		%util：一般地，如果该参数是100%表示设备已经接近满负荷运行了
	
	最后，除了关注指标外，我们更需要结合部署的业务进行分析。对于磁盘随机读写频繁的业务，比如图片存取、数据库、邮件服务器等，此类业务吗，tps才是关键点。对于顺序读写频繁的业务，需要传输大块数据的，如视频点播、文件同步，关注的是磁盘的吞吐量。		