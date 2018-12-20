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

	 