# Linux 命令-资源管理
[Linux 命令大全](http://man.linuxde.net/)

## 磁盘管理
- [df](#df)
- [du](#du)
- [badblock](#badblock)

## 性能监测与优化
- [free](#free)
- [uptime](#uptime)
- [lsb_release](#lsb_release)
- [uname](#uname)

### df
> df命令用于显示磁盘分区上的可使用的磁盘空间。默认显示单位为KB

#### 语法
	df(选项)(参数)
	
#### 选项

	-a或--all：包含全部的文件系统；
	--block-size=<区块大小>：以指定的区块大小来显示区块数目；
	-h或--human-readable：以可读性较高的方式来显示信息；
	-H或--si：与-h参数相同，但在计算时是以1000 Bytes为换算单位而非1024 Bytes；
	-i或--inodes：显示inode的信息；
	-k或--kilobytes：指定区块大小为1024字节；
	-l或--local：仅显示本地端的文件系统；
	-m或--megabytes：指定区块大小为1048576字节；
	--no-sync：在取得磁盘使用信息前，不要执行sync指令，此为预设值；
	-P或--portability：使用POSIX的输出格式；
	--sync：在取得磁盘使用信息前，先执行sync指令；
	-t<文件系统类型>或--type=<文件系统类型>：仅显示指定文件系统类型的磁盘信息；
	-T或--print-type：显示文件系统的类型；
	-x<文件系统类型>或--exclude-type=<文件系统类型>：不要显示指定文件系统类型的磁盘信息；
	--help：显示帮助；
	--version：显示版本信息。
	
### du
> 对文件和目录磁盘使用的空间的查看

#### 语法
	du [选项][文件]
	
#### 选项

	-a或-all 显示目录中个别文件的大小。
	-b或-bytes 显示目录或文件大小时，以byte为单位。
	-c或--total 除了显示个别目录或文件的大小外，同时也显示所有目录或文件的总和。
	-k或--kilobytes 以KB(1024bytes)为单位输出。
	-m或--megabytes 以MB为单位输出。
	-s或--summarize 仅显示总计，只列出最后加总的值。
	-h或--human-readable 以K，M，G为单位，提高信息的可读性。
	-x或--one-file-xystem 以一开始处理时的文件系统为准，若遇上其它不同的文件系统目录则略过。
	-L<符号链接>或--dereference<符号链接> 显示选项中所指定符号链接的源文件大小。
	-S或--separate-dirs 显示个别目录的大小时，并不含其子目录的大小。
	-X<文件>或--exclude-from=<文件> 在<文件>指定目录或文件。
	--exclude=<目录或文件> 略过指定的目录或文件。
	-D或--dereference-args 显示指定符号链接的源文件大小。
	-H或--si 与-h参数相同，但是K，M，G是以1000为换算单位。
	-l或--count-links 重复计算硬件链接的文件。
	
### badblock
> 用于查找磁盘中损坏的区块

#### 语法

	badblock(选项)(参数)

#### 选项

	-b<区块大小>：指定磁盘的区块大小，单位为字节；
	-o<输出文件>：将检查的结果写入指定的输出文件；
	-s：在检查时显示进度；
	-v：执行时显示详细的信息；
	-w：在检查时，执行写入测试。
	
#### 参数

* 磁盘装置：指定要检查的磁盘装置；
* 磁盘区块数：指定磁盘装置的区块总数；
* 启始区块：指定要从哪个区块开始检查。

### free
> free命令可以显示当前系统未使用的和已使用的内存数目，还可以显示被内核使用的内存缓冲区

#### 选项

	-b：以Byte为单位显示内存使用情况；
	-k：以KB为单位显示内存使用情况；
	-m：以MB为单位显示内存使用情况；
	-o：不显示缓冲区调节列；
	-s<间隔秒数>：持续观察内存使用状况；
	-t：显示内存总和列；
	-V：显示版本信息。
#### 实例

	free -m
	             total       used       free     shared    buffers     cached
	Mem:          2016       1973         42          0        163       1497
	-/+ buffers/cache:        312       1703
	Swap:         4094          0       4094
	
第一部分Mem行解释：

	total：内存总数；
	used：已经使用的内存数；
	free：空闲的内存数；
	shared：当前已经废弃不用；
	buffers Buffer：缓存内存数；
	cached Page：缓存内存数。
	
关系：total = used + free

第二部分(-/+ buffers/cache)解释:
	
	(-buffers/cache) used内存数：第一部分Mem行中的 used – buffers – cached
	(+buffers/cache) free内存数: 第一部分Mem行中的 free + buffers + cached
	
可见-buffers/cache反映的是被程序实实在在吃掉的内存，而+buffers/cache反映的是可以挪用的内存总数。


### uptime

#### 选项

	-V：显示指令的版本信息。
	
#### 实例
使用uptime命令查看系统负载：

	[root@LinServ-1 ~]# uptime -V    #显示uptime命令版本信息
	procps version 3.2.7
	
	[root@LinServ-1 ~]# uptime
	 15:31:30 up 127 days,  3:00,  1 user,  load average: 0.00, 0.00, 0.00
显示内容说明：

	15:31:30             //系统当前时间
	up 127 days,  3:00   //主机已运行时间,时间越大，说明你的机器越稳定。
	1 user               //用户连接数，是总连接数而不是用户数
	load average: 0.00, 0.00, 0.00         // 系统平均负载，统计最近1，5，15分钟的系统平均负载
那么什么是系统平均负载呢？ 系统平均负载是指在特定时间间隔内运行队列中的平均进程数。

如果每个CPU内核的当前活动进程数不大于3的话，那么系统的性能是良好的。如果每个CPU内核的任务数大于5，那么这台机器的性能有严重问题。

如果你的linux主机是1个双核CPU的话，当Load Average 为6的时候说明机器已经被充分使用了。

### lsb_release
> lsb_release命令用来显示LSB和特定版本的相关信息

### 选项

	-v 显示版本信息。
	-i 显示发行版的id。
	-d 显示该发行版的描述信息。
	-r 显示当前系统是发行版的具体版本号。
	-c 发行版代号。
	-a 显示上面的所有信息。
	-h 显示帮助信息。
	
### uname
> 用于打印当前系统相关信息（内核版本号、硬件架构、主机名称和操作系统类型等

#### 选项

	-a或--all：显示全部的信息；
	-m或--machine：显示电脑类型；
	-n或-nodename：显示在网络上的主机名称；
	-r或--release：显示操作系统的发行编号；
	-s或--sysname：显示操作系统名称；
	-v：显示操作系统的版本；
	-p或--processor：输出处理器类型或"unknown"；
	-i或--hardware-platform：输出硬件平台或"unknown"；
	-o或--operating-system：输出操作系统名称；
	--help：显示帮助；
	--version：显示版本信息。

