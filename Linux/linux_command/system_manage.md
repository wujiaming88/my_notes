# Linux 命令-系统管理
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
- [tcpdump](#tcpdump)
- [sed](#sed)
- [awk](#awk)
- [grep](#grep)
- [netstat](#netstat)
- [ss](#ss)
- [ps](#ps)
- [top](#top)
- [xargs](#xargs)
- [killall](#killall)


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
> 是一种流编辑器，它是文本处理中非常中的工具，能够完美的配合正则表达式使用。处理时，把当前处理的行存储在临时缓冲区中，称为“模式空间”（pattern space），接着用sed命令处理缓冲区中的内容，处理完成后，把缓冲区的内容送往屏幕。接着处理下一行，这样不断重复，直到文件末尾。文件内容并没有 改变，除非你使用重定向存储输出。Sed主要用来自动编辑一个或多个文件；简化对文件的反复操作；编写转换程序等。

#### 命令格式

	sed [options] 'command' file(s)
	sed [options] -f scriptfile file(s)
	
#### 选项
	
	-e<script>或--expression=<script>：以选项中的指定的script来处理输入的文本文件；
	-f<script文件>或--file=<script文件>：以选项中指定的script文件来处理输入的文本文件；
	-h或--help：显示帮助；
	-n或--quiet或——silent：仅显示script处理后的结果；
	-V或--version：显示版本信息。
	
#### sed 命令

	a\ 在当前行下面插入文本。
	i\ 在当前行上面插入文本。
	c\ 把选定的行改为新的文本。
	d 删除，删除选择的行。
	D 删除模板块的第一行。
	s 替换指定字符
	h 拷贝模板块的内容到内存中的缓冲区。
	H 追加模板块的内容到内存中的缓冲区。
	g 获得内存缓冲区的内容，并替代当前模板块中的文本。
	G 获得内存缓冲区的内容，并追加到当前模板块文本的后面。
	l 列表不能打印字符的清单。
	n 读取下一个输入行，用下一个命令处理新的行而不是用第一个命令。
	N 追加下一个输入行到模板块后面并在二者间嵌入一个新行，改变当前行号码。
	p 打印模板块的行。
	P(大写) 打印模板块的第一行。
	q 退出Sed。
	b lable 分支到脚本中带有标记的地方，如果分支不存在则分支到脚本的末尾。
	r file 从file中读行。
	t label if分支，从最后一行开始，条件一旦满足或者T，t命令，将导致分支到带有标号的命令处，或者到脚本的末尾。
	T label 错误分支，从最后一行开始，一旦发生错误或者T，t命令，将导致分支到带有标号的命令处，或者到脚本的末尾。
	w file 写并追加模板块到file末尾。  
	W file 写并追加模板块的第一行到file末尾。  
	! 表示后面的命令对所有没有被选定的行发生作用。  
	= 打印当前行号码。  
	# 把注释扩展到下一个换行符以前。
	
#### sed 替换标记

	g 表示行内全面替换。  
	p 表示打印行。  
	w 表示把行写入一个文件。  
	x 表示互换模板块中的文本和缓冲区中的文本。  
	y 表示把一个字符翻译为另外的字符（但是不用于正则表达式）
	\1 子串匹配标记
	& 已匹配字符串标记
	
#### sed 元字符集

	^ 匹配行开始，如：/^sed/匹配所有以sed开头的行。
	$ 匹配行结束，如：/sed$/匹配所有以sed结尾的行。
	. 匹配一个非换行符的任意字符，如：/s.d/匹配s后接一个任意字符，最后是d。
	* 匹配0个或多个字符，如：/*sed/匹配所有模板是一个或多个空格后紧跟sed的行。
	[] 匹配一个指定范围内的字符，如/[ss]ed/匹配sed和Sed。  
	[^] 匹配一个不在指定范围内的字符，如：/[^A-RT-Z]ed/匹配不包含A-R和T-Z的一个字母开头，紧跟ed的行。
	\(..\) 匹配子串，保存匹配的字符，如s/\(love\)able/\1rs，loveable被替换成lovers。
	& 保存搜索字符用来替换其他字符，如s/love/**&**/，love这成**love**。
	\< 匹配单词的开始，如:/\<love/匹配包含以love开头的单词的行。
	\> 匹配单词的结束，如/love\>/匹配包含以love结尾的单词的行。
	x\{m\} 重复字符x，m次，如：/0\{5\}/匹配包含5个0的行。
	x\{m,\} 重复字符x，至少m次，如：/0\{5,\}/匹配至少有5个0的行。
	x\{m,n\} 重复字符x，至少m次，不多于n次，如：/0\{5,10\}/匹配5~10个0的行。
	
#### sed 用法实例

##### 替换操作：s命令

	sed 's/book/books/' file	#替换文本中的字符串
	sed -n 's/test/TEST/p' file	#-n选项和p命令一起使用表示只打印那些发生替换的行
	sed -i 's/book/books/g' file 	#直接编辑文件选项-i，会匹配file文件中每一行的第一个book替换为books
	
##### 全面替换标记 g

	sed 's/book/books/g' file	#使用后缀 /g 标记会替换每一行中的所有匹配
	echo sksksksksksk | sed 's/sk/SK/2g'	   #当需要从第N处匹配开始替换时，可以使用 /Ng
		skSKSKSKSKSK

	echo sksksksksksk | sed 's/sk/SK/3g'
		skskSKSKSKSK

	echo sksksksksksk | sed 's/sk/SK/4g'
		skskskSKSKSK
		
##### 定界符
	
	sed 's:test:TEXT:g'	#以上命令中字符 / 在sed中作为定界符使用，也可以使用任意的定界符
	sed 's|test|TEXT|g'
	
	sed 's/\/bin/\/usr\/local\/bin/g' 	#定界符出现在样式内部时，需要进行转义
	
##### 删除操作：d命令

	sed '/^$/d' file 	#删除空白行
	sed '2d' file 	#删除文件的第2行
	sed '2,$d' file 	#删除文件的第2行到末尾所有行
	sed '$d' file 	#删除文件最后一行
	sed '/^test/'d file 	#删除文件中所有开头是test的行
	
##### 已匹配字符串标记&

	echo this is a test line | sed 's/\w\+/[&]/g' #正则表达式 \w\+ 匹配每一个单词，使用 [&] 替换它，& 对应于之前所匹配到的单词
	[this] [is] [a] [test] [line]
	
	sed 's/^192.168.0.1/&localhost/' file  #所有以192.168.0.1开头的行都会被替换成它自已加localhost	192.168.0.1localhost
	
##### 子串匹配标记\1

	echo this is digit 7 in a number | sed 's/digit \([0-9]\)/\1/'    #匹配给定样式的其中一部分
	this is 7 in a number
	
	echo aaa BBB | sed 's/\([a-z]\+\) \([A-Z]\+\)/\2 \1/' #对于匹配到的第一个子串就标记为 \1，依此类推匹配到的第二个结果就是 \2	
	BBB aaa
	
##### 组合多个表达式

	sed '表达式' | sed '表达式'

	等价于：
	
	sed '表达式; 表达式'
	
	 
##### 引用
sed表达式可以使用单引号来引用，但是如果表达式内部包含变量字符串，就需要使用双引号
	
	test=hello
	echo hello WORLD | sed "s/$test/HELLO"
	HELLO WORLD
	
##### 选定行的范围：,（逗号）

	sed -n '/test/,/check/p' file 	#所有在模板test和check所确定的范围内的行都被打印
	sed -n '5,/^test/p' file 	#打印从第5行开始到第一个包含以test开始的行之间的所有行
	sed '/test/,/west/s/$/aaa bbb/' file    #对于模板test和west之间的行，每行的末尾用字符串aaa bbb替换
	
##### 多点编辑：e命令
-e选项允许在同一行里执行多条命令

	sed -e '1,5d' -e 's/test/check/' file     #sed表达式的第一条命令删除1至5行，第二条命令用check替换test。命令的执行顺序对结果有影响。如果两个命令都是替换命令，那么第一个替换命令将影响第二个替换命令的结果
	
	sed --expression='s/test/check/' --expression='/love/d' file     # -e 等价的命令是 --expression
	
##### 从文件读入：r命令

	sed '/test/r file' filename     #file里的内容被读进来，显示在与test匹配的行后面，如果匹配多行，则file的内容将显示在所有匹配行的下面
	
##### 写入文件：w 命令

	sed -n '/test/w file' example 	#在example中所有包含test的行都被写入file里
	
##### 追加（行下）：a\命令

	sed '/^test/a\this is a test line' file     #将 this is a test line 追加到 以test 开头的行后面
	sed -i '2a\this is a test line' test.conf   #在 test.conf 文件第2行之后插入 this is a test line
	
##### 插入（行上）：i\命令

	sed '/^test/i\this is a test line' file     #将 this is a test line 追加到以test开头的行前面
	sed -i '5i\this is a test line' test.conf   #在test.conf文件第5行之前插入this is a test line
	
##### 下一个：n 命令

	sed '/test/{ n; s/aa/bb/; }' file 	#如果test被匹配，则移动到匹配行的下一行，替换这一行的aa，变为bb，并打印该行，然后继续
	
##### 变形：y 命令

	sed '1,10y/abcde/ABCDE/' file 	#把1~10行内所有abcde转变为大写，注意，正则表达式元字符不能使用这个命令
	
##### 退出：q命令

	sed '10q' file  		#打印完第10行后，退出sed

##### 脚本 scriptfile
sed脚本是一个sed的命令清单，启动Sed时以-f选项引导脚本文件名。Sed对于脚本中输入的命令非常挑剔，在命令的末尾不能有任何空白或文本，如果在一行中有多个命令，要用分号分隔。以#开头的行为注释行，且不能跨行

	sed [options] -f scriptfile file(s)


### awk
### grep
> 能使用正则表达式搜索文本，并把匹配的行打印出来

#### 选项

	-a 不要忽略二进制数据。
	-A<显示列数> 除了显示符合范本样式的那一行之外，并显示该行之后的内容。
	-b 在显示符合范本样式的那一行之外，并显示该行之前的内容。
	-c 计算符合范本样式的列数。
	-C<显示列数>或-<显示列数>  除了显示符合范本样式的那一列之外，并显示该列之前后的内容。
	-d<进行动作> 当指定要查找的是目录而非文件时，必须使用这项参数，否则grep命令将回报信息并停止动作。
	-e<范本样式> 指定字符串作为查找文件内容的范本样式。
	-E 将范本样式为延伸的普通表示法来使用，意味着使用能使用扩展正则表达式。
	-f<范本文件> 指定范本文件，其内容有一个或多个范本样式，让grep查找符合范本条件的文件内容，格式为每一列的范本样式。
	-F 将范本样式视为固定字符串的列表。
	-G 将范本样式视为普通的表示法来使用。
	-h 在显示符合范本样式的那一列之前，不标示该列所属的文件名称。
	-H 在显示符合范本样式的那一列之前，标示该列的文件名称。
	-i 忽略字符大小写的差别。
	-l 列出文件内容符合指定的范本样式的文件名称。
	-L 列出文件内容不符合指定的范本样式的文件名称。
	-n 在显示符合范本样式的那一列之前，标示出该列的编号。
	-q 不显示任何信息。
	-R/-r 此参数的效果和指定“-d recurse”参数相同。
	-s 不显示错误信息。
	-v 反转查找。
	-w 只显示全字符合的列。
	-x 只显示全列符合的列。
	-y 此参数效果跟“-i”相同。
	-o 只输出文件中匹配到的部分。
	
#### 常见用法

在文件中搜索一个单词，命令会返回一个包含"match_pattern"的文本行：

	grep match_pattern file_name
	grep "match_pattern" file_name
	
在多个文件查找：
	
	grep "match_pattern" file_1 file_2 file_3 ...
	
输出除之外的所有行 -v 选项：

	grep -v "match_pattern" file_name
	
标记匹配颜色 --color=auto 选项：

	grep "match_pattern" file_name --color=auto
	
使用正则表达式 -E 选项：

	grep -E "[1-9]+"
	或
	egrep "[1-9]+"
	
只输出文件中匹配到的部分 -o 选项：

	echo this is a test line. | grep -o -E "[a-z]+\."
	line.
	
	echo this is a test line. | egrep -o "[a-z]+\."
	line.
	
统计文件或者文本中包含匹配字符串的行数 -c 选项:

	grep -c "text" file_name
	
输出包含匹配字符串的行数 -n 选项：

	grep "text" -n file_name
	cat file_name | grep "text" -n
	
	# 多个文件
	grep "text" -n file_1 file_2
	
搜索多个文件并查找匹配文本在哪些文件中:

	grep -l "text" file1 file2 file3...
	
#### 递归搜索

在多级目录中对文本进行递归搜索:

	grep "text" . -r -n
	
忽略匹配样式中的字符大小写：

	echo "hello world" | grep -i "HELLO"
	
在 grep 搜索结果中包括或者排除指定文件:

	#只在目录中所有的.php和.html文件中递归搜索字符"main()"
	grep "main()" . -r --include *.{php,html}
	
	#在搜索结果中排除所有README文件
	grep "main()" . -r --exclude "README"
	
	#在搜索结果中排除filelist文件列表里的文件
	grep "main()" . -r --exclude-from filelist
	


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
	
### ss
> ss命令用来显示处于活动状态的套接字信息。ss命令可以用来获取socket统计信息，它可以显示和netstat类似的内容。但ss的优势在于它能够显示更多更详细的有关TCP和连接状态的信息，而且比netstat更快速更高效
> > ss快的秘诀在于，它利用到了TCP协议栈中tcp_diag(tcp_diag是一个用于分析统计的模块)

#### 选项

	-h：显示帮助信息；
	-V：显示指令版本信息；
	-n：不解析服务名称，以数字方式显示；
	-a：显示所有的套接字；
	-l：显示处于监听状态的套接字；
	-o：显示计时器信息；
	-m：显示套接字的内存使用情况；
	-p：显示使用套接字的进程信息；
	-i：显示内部的TCP信息；
	-4：只显示ipv4的套接字；
	-6：只显示ipv6的套接字；
	-t：只显示tcp套接字；
	-u：只显示udp套接字；
	-d：只显示DCCP套接字；
	-w：仅显示RAW套接字；
	-x：仅显示UNIX域套接字。
	
#### 实例

	ss -t -a 	#显示 TCP 连接
	ss -s 		#显示 Sockets 摘要(列出当前的established, closed, orphaned and waiting TCP sockets)
	ss -pl		#查看进程使用的 socket
	ss -pl | grep 3306 	#找出打开套接字/端口应用程序
	ss -u -a 	#显示所有 UDP Sockets
	

### ps
> ps命令用于报告当前系统的进程状态.可以搭配kill指令随时中断、删除不必要的程序
> ps命令是最基本同时也是非常强大的进程查看命令，使用该命令可以确定有哪些进程正在运行和运行的状态、进程是否结束、进程有没有僵死、哪些进程占用了过多的资源等等

#### 选项

	-a：显示所有终端机下执行的程序，除了阶段作业领导者之外。
	a：显示现行终端机下的所有程序，包括其他用户的程序。
	-A：显示所有程序。
	-c：显示CLS和PRI栏位。
	c：列出程序时，显示每个程序真正的指令名称，而不包含路径，选项或常驻服务的标示。
	-C<指令名称>：指定执行指令的名称，并列出该指令的程序的状况。
	-d：显示所有程序，但不包括阶段作业领导者的程序。
	-e：此选项的效果和指定"A"选项相同。
	e：列出程序时，显示每个程序所使用的环境变量。
	-f：显示UID,PPIP,C与STIME栏位。
	f：用ASCII字符显示树状结构，表达程序间的相互关系。
	-g<群组名称>：此选项的效果和指定"-G"选项相同，当亦能使用阶段作业领导者的名称来指定。
	g：显示现行终端机下的所有程序，包括群组领导者的程序。
	-G<群组识别码>：列出属于该群组的程序的状况，也可使用群组名称来指定。
	h：不显示标题列。
	-H：显示树状结构，表示程序间的相互关系。
	-j或j：采用工作控制的格式显示程序状况。
	-l或l：采用详细的格式来显示程序状况。
	L：列出栏位的相关信息。
	-m或m：显示所有的执行绪。
	n：以数字来表示USER和WCHAN栏位。
	-N：显示所有的程序，除了执行ps指令终端机下的程序之外。
	-p<程序识别码>：指定程序识别码，并列出该程序的状况。
	p<程序识别码>：此选项的效果和指定"-p"选项相同，只在列表格式方面稍有差异。
	r：只列出现行终端机正在执行中的程序。
	-s<阶段作业>：指定阶段作业的程序识别码，并列出隶属该阶段作业的程序的状况。
	s：采用程序信号的格式显示程序状况。
	S：列出程序时，包括已中断的子程序资料。
	-t<终端机编号>：指定终端机编号，并列出属于该终端机的程序的状况。
	t<终端机编号>：此选项的效果和指定"-t"选项相同，只在列表格式方面稍有差异。
	-T：显示现行终端机下的所有程序。
	-u<用户识别码>：此选项的效果和指定"-U"选项相同。
	u：以用户为主的格式来显示程序状况。
	-U<用户识别码>：列出属于该用户的程序的状况，也可使用用户名称来指定。
	U<用户名称>：列出属于该用户的程序的状况。
	v：采用虚拟内存的格式显示程序状况。
	-V或V：显示版本信息。
	-w或w：采用宽阔的格式来显示程序状况。　
	x：显示所有程序，不以终端机来区分。
	X：采用旧式的Linux i386登陆格式显示程序状况。
	-y：配合选项"-l"使用时，不显示F(flag)栏位，并以RSS栏位取代ADDR栏位　。
	-<程序识别码>：此选项的效果和指定"p"选项相同。
	--cols<每列字符数>：设置每列的最大字符数。
	--columns<每列字符数>：此选项的效果和指定"--cols"选项相同。
	--cumulative：此选项的效果和指定"S"选项相同。
	--deselect：此选项的效果和指定"-N"选项相同。
	--forest：此选项的效果和指定"f"选项相同。
	--headers：重复显示标题列。
	--help：在线帮助。
	--info：显示排错信息。
	--lines<显示列数>：设置显示画面的列数。
	--no-headers：此选项的效果和指定"h"选项相同，只在列表格式方面稍有差异。
	--group<群组名称>：此选项的效果和指定"-G"选项相同。
	--Group<群组识别码>：此选项的效果和指定"-G"选项相同。
	--pid<程序识别码>：此选项的效果和指定"-p"选项相同。
	--rows<显示列数>：此选项的效果和指定"--lines"选项相同。
	--sid<阶段作业>：此选项的效果和指定"-s"选项相同。
	--tty<终端机编号>：此选项的效果和指定"-t"选项相同。
	--user<用户名称>：此选项的效果和指定"-U"选项相同。
	--User<用户识别码>：此选项的效果和指定"-U"选项相同。
	--version：此选项的效果和指定"-V"选项相同。
	--widty<每列字符数>：此选项的效果和指定"-cols"选项相同。

### top
> top命令可以实时动态地查看系统的整体运行情况

#### 选项

	-b：以批处理模式操作；
	-c：显示完整的治命令；
	-d：屏幕刷新间隔时间；
	-I：忽略失效过程；
	-s：保密模式；
	-S：累积模式；
	-i<时间>：设置间隔时间；
	-u<用户名>：指定用户名；
	-p<进程号>：指定进程；
	-n<次数>：循环显示的次数。
	
#### top交互命令
> 如果在命令行中使用了-s选项， 其中一些命令可能会被屏蔽

	h：显示帮助画面，给出一些简短的命令总结说明；
	k：终止一个进程；
	i：忽略闲置和僵死进程，这是一个开关式命令；
	q：退出程序；
	r：重新安排一个进程的优先级别；
	S：切换到累计模式；
	s：改变两次刷新之间的延迟时间（单位为s），如果有小数，就换算成ms。输入0值则系统将不断刷新，默认值是5s；
	f或者F：从当前显示中添加或者删除项目；
	o或者O：改变显示项目的顺序；
	l：切换显示平均负载和启动时间信息；
	m：切换显示内存信息；
	t：切换显示进程和CPU状态信息；
	c：切换显示命令名称和完整命令行；
	M：根据驻留内存大小进行排序；
	P：根据CPU使用百分比大小进行排序；
	T：根据时间/累计时间进行排序；
	w：将当前设置写入~/.toprc文件中。
	
	
### xargs
> xargs命令是给其他命令传递参数的一个过滤器，也是组合多个命令的一个工具

> 它擅长将标准输入数据转换成命令行参数，xargs能够处理管道或者stdin并将其转换成特定命令的命令参数
 
> xargs也可以将单行或多行文本输入转换为其他格式，例如多行变单行，单行变多行

> xargs的默认命令是echo，空格是默认定界符

#### 用法
##### xargs用作替换工具，读取输入数据重新格式化后输出

定义一个测试文件，内有多行文本数据：

	cat test.txt
	
	a b c d e f g
	h i j k l m n
	o p q
	r s t
	u v w x y z

多行输入单行输出：

	cat test.txt | xargs
	
	a b c d e f g h i j k l m n o p q r s t u v w x y z

##### -n选项多行输出

	cat test.txt | xargs -n3
	
	a b c
	d e f
	g h i
	j k l
	m n o
	p q r
	s t u
	v w x
	y z
	
##### -d选项可以自定义一个定界符

	echo "nameXnameXnameXname" | xargs -dX
	
	name name name name
	
结合-n选项使用：

	echo "nameXnameXnameXname" | xargs -dX -n2
	
	name name
	name name

##### -I 选项
使用-I指定一个替换字符串{}，这个字符串在xargs扩展时会被替换掉，当-I与xargs结合使用，每一个参数命令都会被执行一次

	cat arg.txt | xargs -I {} ./sk.sh -p {} -l
	
	-p aaa -l
	-p bbb -l
	-p ccc -l
	
复制所有图片文件到 /data/images 目录下：

	ls *.jpg | xargs -n1 -I cp {} /data/images
	

##### xargs结合find使用

用rm 删除太多的文件时候，可能得到一个错误信息：/bin/rm Argument list too long. 用xargs去避免这个问题：

	find . -type f -name "*.log" -print0 | xargs -0 rm -f
xargs -0将\0作为定界符。

统计一个源代码目录中所有php文件的行数：

	find . -type f -name "*.php" -print0 | xargs -0 wc -l
查找所有的jpg 文件，并且压缩它们：

	find . -type f -name "*.jpg" -print | xargs tar -czvf images.tar.gz


### killall
> killall命令使用进程的名称来杀死进程，使用此指令可以杀死一组同名进程

#### 选项

	-e：对长名称进行精确匹配；
	-l：忽略大小写的不同；
	-p：杀死进程所属的进程组；
	-i：交互式杀死进程，杀死进程前需要进行确认；
	-l：打印所有已知信号列表；
	-q：如果没有进程被杀死。则不输出任何信息；
	-r：使用正规表达式匹配要杀死的进程名称；
	-s：用指定的进程号代替默认信号“SIGTERM”；
	-u：杀死指定用户的进程。






	 