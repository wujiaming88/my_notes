# Linux 命令
[Linux 命令大全](http://man.linuxde.net/)

## 常用

| 命令 | 说明 |
| :------ | :------ |
| mv | 移动文件/目录，重命名 |
| cp | 复制文件/目录 |
| find | 查找文件 |
| locate | 查找文件 |
| head | 显示文件前10行(-n 可指定显示多少行）|
| tail | 显示文件后10行文件(-n 可指定显示多少行) |
| mkdir | 创建目录 |
| touch | 创建文件 |
| chomd | 更改文件或者目录的全选 |
| gzip | 压缩文件 |
| gunzip | 解压缩文件 |
| tar | 打包/解包 |
| which/whereis | 查找命令所在路径 |

## 高级
### tcpdump
> tcpdump命令是一款sniffer工具，它可以打印所有经过网络接口的数据包的头信息，也可以使用`-w`选项将数据包保存到文件中，方便以后分析

	-a：尝试将网络和广播地址转换成名称；
	-c<数据包数目>：收到指定的数据包数目后，就停止进行倾倒操作；
	-d：把编译过的数据包编码转换成可阅读的格式，并倾倒到标准输出；
	-dd：把编译过的数据包编码转换成C语言的格式，并倾倒到标准输出；
	-ddd：把编译过的数据包编码转换成十进制数字的格式，并倾倒到标准输出；
	-e：在每列倾倒资料上显示连接层级的文件头；
	-f：用数字显示网际网络地址；
	-F<表达文件>：指定内含表达方式的文件；
	-i<网络界面>：使用指定的网络截面送出数据包；
	-l：使用标准输出列的缓冲区；
	-n：不把主机的网络地址转换成名字；
	-N：不列出域名；
	-O：不将数据包编码最佳化；
	-p：不让网络界面进入混杂模式；
	-q ：快速输出，仅列出少数的传输协议信息；
	-r<数据包文件>：从指定的文件读取数据包数据；
	-s<数据包大小>：设置每个数据包的大小；
	-S：用绝对而非相对数值列出TCP关联数；
	-t：在每列倾倒资料上不显示时间戳记；
	-tt： 在每列倾倒资料上显示未经格式化的时间戳记；
	-T<数据包类型>：强制将表达方式所指定的数据包转译成设置的数据包类型；
	-v：详细显示指令执行过程；
	-vv：更详细显示指令执行过程；
	-x：用十六进制字码列出数据包资料；
	-w<数据包文件>：把数据包数据写入指定的文件。
	
#### 监视指定主机的数据包

	tcpdump host sundown		打印所有进入或离开sundown的数据包
	tcpdump host 210.27.48.1	截获所有210.27.48.1 的主机收到的和发出的所有的数据包
	tcpdump host helios and \( hot or ace \)    打印helios 与 hot 或者与 ace 之间通信的数据包
	tcpdump host 210.27.48.1 and \ (210.27.48.2 or 210.27.48.3 \) 截获主机210.27.48.1 和主机210.27.48.2 或210.27.48.3的通信
	tcpdump ip host ace and not helios	打印ace与任何其他主机之间通信的IP 数据包, 但不包括与helios之间的数据包
	tcpdump ip host 210.27.48.1 and ! 210.27.48.2    获取主机210.27.48.1除了和主机210.27.48.2之外所有主机通信的ip包
	tcpdump -i eth0 src host hostname		截获主机hostname发送的所有数据
	tcpdump -i eth0 dst host hostname		监视所有送到主机hostname的数据包
	
#### 监视指定主机和端口的数据包

	tcpdump tcp port 23 host 210.27.48.1	   如果想要获取主机210.27.48.1接收或发出的telnet包，使用如下命令
	tcpdump udp port 123 	对本机的udp 123 端口进行监视 123 为ntp的服务端口


### sed
### awk
### grep
### netstat

> 用来打印Linux中网络系统的状态信息，可让你得知整个Linux系统的网络情况

	-a或--all：显示所有连线中的Socket；
	 -A<网络类型>或--<网络类型>：列出该网络类型连线中的相关地址；
	 -c或--continuous：持续列出网络状态；
	 -C或--cache：显示路由器配置的快取信息；
	 -e或--extend：显示网络其他相关信息；
	 -F或--fib：显示FIB；
	 -g或--groups：显示多重广播功能群组组员名单；
	 -h或--help：在线帮助；
	 -i或--interfaces：显示网络界面信息表单；
	 -l或--listening：显示监控中的服务器的Socket；
	 -M或--masquerade：显示伪装的网络连线；
	 -n或--numeric：直接使用ip地址，而不通过域名服务器；
	 -N或--netlink或--symbolic：显示网络硬件外围设备的符号连接名称；
	 -o或--timers：显示计时器；
	 -p或--programs：显示正在使用Socket的程序识别码和程序名称；
	 -r或--route：显示Routing Table；
	 -s或--statistice：显示网络工作信息统计表；
	 -t或--tcp：显示TCP传输协议的连线状况；
	 -u或--udp：显示UDP传输协议的连线状况；
	 -v或--verbose：显示指令执行过程；
	 -V或--version：显示版本信息；
	 -w或--raw：显示RAW传输协议的连线状况；
	 -x或--unix：此参数的效果和指定"-A unix"参数相同；
	 --ip或--inet：此参数的效果和指定"-A inet"参数相同。
	
#### 列出所有端口

	netstat -a     #列出所有端口
	netstat -at    #列出所有tcp端口
	netstat -au    #列出所有udp端口 
	
#### 列出所有处于监听状态的Sockets

	netstat -l        #只显示监听端口
	netstat -lt       #只列出所有监听 tcp 端口
	netstat -lu       #只列出所有监听 udp 端口
	netstat -lx       #只列出所有监听 UNIX 端口
	
#### 显示每个协议的统计信息

	netstat -s   显示所有端口的统计信息
	netstat -st   显示TCP端口的统计信息
	netstat -su   显示UDP端口的统计信息
	
#### 在netstat输出中显示 PID 和进程名称

	netstat -pt 显示TCP端口的PID和进程名称
	netstat -pu 显示UDP端口的PID和进程名称
	
`netstat -p`可以与其它开关一起使用，就可以添加“PID/进程名称”到netstat输出中

#### 找出程序运行的端口
并不是所有的进程都能找到，没有权限的会不显示，使用 root 权限查看所有的信息

	netstat -ap | grep ssh
	
#### 找出运行在指定端口的进程

	netstat -an | grep ':80'
	
#### 显示网络接口列表

	netstat -i
	netstat -ie  显示详细信息
	
#### TCP/IP分析

	查看连接某服务端口最多的的IP地址：
	netstat -ntu | grep :80 | awk '{print $5}' | cut -d: -f1 | awk '{++ip[$1]} END {for(i in ip) print ip[i],"\t",i}' | sort -nr
	
	TCP各种状态列表：
	netstat -nt | grep -e 127.0.0.1 -e 0.0.0.0 -e ::: -v | awk '/^tcp/ {++state[$NF]} END {for(i in state) print i,"\t",state[i]}'
	
### SS

	 