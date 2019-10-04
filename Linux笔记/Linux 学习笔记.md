# 目录
[toc]
# 一 Linux系统简介
## 1. 分区类型
* 主分区：最多只能4个分区
* 扩展分区：最多只能一个(主分区+扩展分区最多有4个，不能写入数据，只能包含逻辑分区)
* 逻辑分区

## 2. 格式化(写入文件系统)

## 3. 硬件 设备设备文件名

|设备|设备文件名|
|----|----|
|IDE硬盘|/dev/hd[a-d]|
|SCSI/SATA/USB硬盘|/dev/sd[a-p]|
|光驱|/dev/cdrom或者/dev/sro|
|软盘|/dev/fd[0-1]|
|打印机(25针)|/dev/lp[0-2]|
|打印机(USB)|/dev/usb/lp[0-15]|
|鼠标|/dev/mouse|

## 4. 挂载(盘符)
* 必须分区
	+ / (根分区)
	+ swap分区 (交换分区、内存2倍、不超过2GB)
* 推荐分区
	+ /boot (启动分区 200MB)

## 5. 文件系统

```
		/
		  +--[/boot]
		  +--[/etc]
		      +--[passwd]
		      +--[passwd]
		      +--[group]
		  +--[/home]

```

|/dev/sda1/|/dev/sda2/|/dev/sda3/|
|----|----|----|
|(/boot)|(/home)|(/)|

*** (可以给子目录分配一个磁盘) ***

# 二 系统安装
## 1. 安装欢迎界面
* Install or upgrade an existing system (安装或者升级现有的系统)
* Install system with basic vido driver (安装过程采用基本显卡驱动)
* Resume install system (进入系统修复模式)
* Boot from local drive  (退出安装从硬盘启动)
* Memory test (存储介质检测)

## 2. 软件包选择
* Desktop (桌面)
* Minimal Desktop (最小化桌面)
* Minimal (最小化)
* Basic Server (基本服务器)
* Database Server (数据库服务器)
* Web Server (网页服务器)
* Virtual Host (虚拟主机)
* Software development workstation (软件开发工作站)

## 3. 安装日志
* /root/install.log :储存了安装在系统中的软件包及其版本信息
* /root/install.log.syslog :储存了安装过程中留下的事件记录
* /root/anaconda-ks.cfg :以kickstart配置文件的格式记录它安装过程中设置的选项信息

## 4. 注意事项
* Linux严格区分大小写
* Linux中所有内容以文件形式保存，包括硬件
	+ 硬盘文件是 /dev/sd[a-p]
	+ 光盘文件是 /dev/sr0等
* Linux 不靠扩展名区分文件类型
	+ **Linux的一些扩展名**

	|类型|扩展名|
	|----|----|
	|压缩包|\*.gz 、\*.bz2 、\*.tar.bz2 、*.tgz等
	|二进制软件包|\*.rpm|
	|网页文件|\*.htmp 、*.php|
	|脚本文件|\*.sh|
	|配置文件|\*.conf| 

* Linux所有的存储系统设备都必须挂载之后用户才能使用
* Windows下的程序不能直接在Linux中安装和运行

## 5. Liunx各目录的作用

|目录名|目录作用|
|----|----|
|/bin/|存放系统命令的目录，普通用户和超级用户都可以执行，不过放在/bin/下的命令在单用户模式下也可以执行|
|/sbin/|保存与系统环境变量相关的命令，只有超级用户可以使用这些命令进行环境设置，但是有些命令可以允许普通用户查看|
|/usr/bin/|存放系统命令的目录，普通用户和超级用户都可以执行，这些命令和系统启动无关，在单用户模式下不能执行|
|/usr/sbin/|存放根文件系统不必要的系统管理命令，例如多数服务程序。只有超级用户可以使用。大家其实注意到Linux的系统，在所有"sbin"目录中保存的命令只有超级用户可以使用，"bin"目录中保存的命令所有用户可以使用|
|/boot/|系统启动目录，保存系统启动相关的文件，如内核文件和启动引导程序(grub)文件等|
|/dev/|设备文件保存位置，Linux所有内核以文件形式保存，包括硬件，那么这个目录就是用来保存所有硬件设备文件的|
|/etc/|配置文件保存位置，系统内所有采用默认安装方式(rpm安装)的服务的配置文件全部都保存在这个目录中，如用户账号和密码，服务的启动脚本，常用服务的配置文件等|
|/home/|普通用户的家目录。建立每个用户时，每个用户要有一个默认登陆位置，这个位置就是这个用户的家目录，所有普通用户的家目录就是/home 下建立一个和用户名相同的目录，如用户user1的家目录就是/home/user1/|
|/lib/|系统调用的函数库保存位置|
|lost+found/|当系统意外崩溃或机器意外关机，而产生一些文件碎片在这里。当系统启动的过程中fsck工具会只在每个分区中出现，例如/lost+found 就是根分区下的备份恢复目录。/boot/lost+found 就是/boot 分区的备份恢复目录|
|/media/|挂载目录，系统建议是用来挂载媒体设备的，例如软盘和光盘|
|/mnt/|挂载目录，早期Linux中资源这一个挂载目录，并没有细分，现在这个目录系统建议挂载额外设备，如U盘，移动硬盘和其它操作系统的分区|
|/misc/|挂载目录，系统建议用来挂载NFS服务的共享目录(一个已建立的空目录就可以昨晚挂载点，那么系统虽然准备了三个默认挂载目录/media、/mnt、/misc，但是到底在哪个目录挂载什么设备都由管理员自己决定)|
|/opt/|第三方安装的软件保存位置，这个目录就是放置和安装其它软件的位置，手工安装的源码包软件可以安装到这个目录中，(/usr/local/ 目录可以用来安装软件，更习惯安装在/usr/local/ 目录下)|
|/proc/|虚拟文件系统，该目录中的数据并不保存到硬盘当中，而是保存到内存中。主要保存系统的内核，进程，外部设备状态和网络状态等。如/proc/cpuinfo 是保存cpu信息的，/proc/device 是保存设备驱动的列表的，/proc/filesystems 是保存文件系统列表的，/proc/net 是保存网络协议信息的|
|/sys/|虚拟文件系统，和/proc 目录相似，都保存在内存当中的，主要是保存内核相关信息|
|/root/|超级用户的家目录，普通用户家目录在"/home"下，超级用户家目录直接在"/"下|
|/srv/|服务数据目录。一些系统服务启动之后，可以在这个目录中保存所需的数据|
|/tmp/|临时目录。系统存放临时文件的目录，该目录下的所有用户都可以访问和写入。建议此目录下不要保存重要数据，最好没错开机都把该目录清空|
|/usr/|系统软件资源目录，注意"usr"不是"user"的缩写，而是"Unix Software Resource"的缩写，所以不是存放用户数据的，而是存放系统软件资源的目录，系统中安装的软件大多数都保存在这里。|
|/var/|动态数据保存位置，主要保存缓存，日志以及软件运行所产生的文件|

## 6. 服务器注意事项
* 远程服务器不允许关机，只能重启
* 重启时应该关闭服务
* 不要在服务访问高峰运行高负载命令
* 远程配置防火墙时不要把自己踢出服务器
* 指定合理的密码规范并定期更新
* 合理分配权限
* 定期备份重要数据和日志

# 三 常用命令
	命令格式： 命令 [-选项][参数]
	例如:ls -la /etc
	说明:1)个别命令使用不遵循此格式
	     2)当有多个选项时，可以写在一起
	     3)简化项与完整选项-a 等于 --all

## 1. 目录处理命令

### 1.1 ls
	命令名称:ls
		英文原意:ls    命令所在路径:/bin/ls
	执行权限:所有用户
	功能描述:显示目录文件
	语    法:ls 选项[-ald][文件或目录]
			-a 显示所有文件，包括隐藏文件
			-l 详细信息显示
			-d 查看目录属性
			-h 人性化显示字节k或M

**Linux中以"."(点)开头的文件为隐藏文件**

**-rw------- 1 root root 1025 3月3 08:10 xxxx 的解释**

|-|rw-|---|---|1|root|root|1025|3月3 08:10|xxxx|
|----|----|----|----|----|----|----|----|----|----|
|x|x|x|x|调用次数|所有者|所属组|文件大小|最后一次修改时间|文件名|



|-|rw-|---|---|
|----|----|----|----|
|- 二进制文件,d 目录,l 软件链接文件|u 即所属者的权限|g 即所属组的权限|o 即其它人的权限|


|r|w|x|
|----|----|----|
|可读|可写|可执行|

### 1.2 mkdir
	命令名称:mkdir
		英文原意:make directories    命令所在路径:/bin/mkdir
	执行权限:所有用户
	功能描述:创建新目录
	语    法:mkdir -p [目录名]
			-p 递归创建新目录

	范    例:
			$ mkdir -p /tmp/sky1/xx2
			$ mkdir /tmp/sky1/test /tmp/sky1/test2

### 1.3 cd 
	命令名称:cd
		英文原意:change directories    命令所在路径:shell 内置命令
	执行权限:所有用户
	功能描述:切换目录
	语    法:cd [目录名]
			
	范    例:
			$ cd /tmp/sky1/test1  切换到指定目录
			$ cd ..               回到上一级目录

### 1.4 pwd
	命令名称:pwd
		英文原意:print working directory    命令所在路径:/bin/pwd
	执行权限:所有用户
	功能描述:显示当前目录
	语    法:$ pwd
			
	范    例:
			$ pwd
			 /tmp/sky1

### 1.5 rmdir
	命令名称:rmdir
		英文原意:remove empty directories    命令所在路径:shell 内置命令
	执行权限:所有用户
	功能描述:删除空目录
	语    法:rmdir [目录名]
			
	范    例:
			$ rmdir /tmp/sky1/test1


### 1.6 cp
	命令名称:cp
		英文原意:copy    命令所在路径:/bin/cp
	执行权限:所有用户
	功能描述:复制文件或目录
	语    法:cp -rp [原文件或目录] [目标目录]
			-r 复制目录
			-p 保留文件属性

	范    例:
			$ cp -r /tmp/sky1/test2  /root
			将目录 /tmp/sky1/test2 复制到目录 /root

			$ cp -rp /tmp/sky1/test1 /tmp/sky1/test1  /root
			将/tmp/sky1目录下的test1 和test2 复制到目录/root 下

			$ cp -r /tmp/sky1/test2 /root/test3
			将/tmp/sky1 目录下的test2 复制到/root 下，并命名为test3


### 1.7 mv
	命令名称:mv
		英文原意:move    命令所在路径:/bin/mv
	执行权限:所有用户
	功能描述:剪切文件、改名
	语    法:mv [原文件或目录] [目标目录]


### 1.8 rm
	命令名称:rm
		英文原意:remove    命令所在路径:/bin/rm
	执行权限:所有用户
	功能描述:删除文件
	语    法:rm -rf [文件或目录]
			-r 删除目录
			-f 强制执行(无询问直接删除)

	范    例:
			$ rm /tmp/yum.log
			删除文件 /tmp/yum.log

			$ rm -rf /tmp/sky1/test1
			删除目录/tmp/sky1/test1

## 2. 文件处理命令

### 2.1 touch
	命令名称:touch
		英文原意:    命令所在路径:/bin/touch
	执行权限:所有用户
	功能描述:创建空文件
	语    法:touch [文件名]
		
	范    例:$ touch skys.list
			 $ touch "sky test"(创建名字带空格的文件)

### 2.2 cat
	命令名称:cat
		英文原意:    命令所在路径:/bin/cat
	执行权限:所有用户
	功能描述:显示文件内容
	语    法:cat [文件名]
			-n 显示行号			
	
	范    例:$ cat /etc/issue
			 $ cat -n /etc/services
			 
** 注tac 可倒着显示文本内容 **

### 2.3 more
	命令名称:more
		英文原意:    命令所在路径:/bin/more
	执行权限:所有用户
	功能描述:分页显示文件内容
	语    法:more [文件名]
			(空格)或f   翻页
			(Enter)     换行
			q或Q        退出	

	范    例:$ more /etc/services

### 2.4 less
	命令名称:less
		英文原意:    命令所在路径:/usr/bin/less
	执行权限:所有用户
	功能描述:分页显示文件内容(可向上翻页)
	语    法:less [文件名]
						
	范    例:$ less /etc/services
	也可以寻找，输入"/" + 寻找内容，按N可以找下一个关键词

### 2.5 head
	命令名称:head
		英文原意:    命令所在路径:/usr/bin/head
	执行权限:所有用户
	功能描述:显示文件前面几行
	语    法:head [文件名]
			-n 指定行数(默认10行)

	范    例:$ head -n 20 /etc/services

### 2.6 tail
	命令名称:tail
		英文原意:   命令所在路径:/usr/bin/tail
	执行权限:所有用户
	功能描述:显示文件后面几行
	语    法:tail [文件名]
			-n 指定行数(默认10行)
			-f 动态显示文件末尾内容

	范    例:$ tail -n 18 /etc/services


## 3. 链接命令

### 3.1 ln
	命令名称:ln
		英文原意:link    命令所在路径:/bin/ln
	执行权限:所有用户
	功能描述:生成链接文件
	语    法:ln -s [原文件] [目标文件]
			-s 创建软链接
			-i 查看i节点

	范    例:$ ln -s /etc/issue /tmp/issue.soft
			创建文件 /etc/issue 的软链接 /tmp/issue.soft

			$ ln /etc/issue /tmp/issue.hard
			创建文件 /etc/issue 的硬链接 /tmp/issue.hard

* 硬连接的特征(类似Windows快捷方式)

	> lrwxrwxrwx 1 root root 10 3月 7:23:39 /tmp/issue.soft -> /etc/issue

	> 1. 权限中lrwxrwxrwx l表示软链接

	> 2. /tmp/issue.soft -> /etc/issue 箭头指向源文件

	> 3. 文件大小——只是符号链接的大小

* 硬链接的特征(源文件丢失，硬链接依然能访问)

	> 1. 拷贝 cp -p + 同步更新(echo "www.lampbrother.net" >> /etc/issue)

	> 2. 通过i节点识别(i节点相当于id)

	> 3. 不能跨分区

	> 4. 不能针对目录使用

## 4. 权限管理命令

### 4.1 chmod
	命令名称:chmod
		英文原意:change the permissions mode of a file    命令所在路径:/bin/chmod
	执行权限:所有用户
	功能描述:改变文件或目录权限
	语    法:chmod [ugoa] {+-=} {rwx} [文件或目录]
			 chmod [mode=421][文件或目录]
			-R 递归修改

	范    例: /tmp下有一个1.txt 权限为-rw-r--r-- ,给拥有者添加x(可执行权限)
			 $ chmod u+x 1.txt

			 给所属组添加写权限，其它人减少读权限
			 $ chmod g+w,o-r 1.txt

			 给所属组设置rwx权限
			 $ chmod g=rwx 1.txt

* 权限的数字表示
	+ r —— 4
	+ w —— 2
	+ x —— 1

	> rwx rw- r--
	
	> (7) (6) (4)

	> 给1.txt 开启所有人的所有权限

	> $ chmod 777 1.txt

* **文件目录权限总结**

 |代表字符|权限|对文件的含义|对目录的含义|
 |----|----|----|----|
 |r|读权限|可以查看文件内容|可以列出目录中的内容|
 |w|写权限|可以修改文件内容|可以在目录中创建、删除文件|
 |x|执行权限|可以执行文件|可以进入目录|

 * **文件权限对应的一些命令**

 |权限|命令|
 |----|----|
 |r|cat、more、head、tail、less|
 |w|vim|
 |x|script command|

  * **目录权限对应的一些命令**

 |权限|命令|
 |----|----|
 |r|ls|
 |w|touch、mkdir、rmdir、rm|
 |x|cd|


### 4.2 chown
	命令名称:chown
		英文原意:change file ownership    命令所在路径:/bin/chown
	执行权限:所有用户
	功能描述:改变文件或目录的所有者
	语    法:chown [用户] [文件或目录]

	范    例:$ chown sky 1.txt
			改变文件1.txt 的所有者为sky (只有root才可以执行)

### 4.3 chgrp
	命令名称:chgrp
		英文原意:change file group ownership    命令所在路径:/bin/chgrp
	执行权限:所有用户
	功能描述:改变文件或目录的所属组
	语    法:chmod [用户组] [文件或目录]

	范    例:$ chgrp sgrp 1.txt
			 改变1.txt的所属组为sgrp

### 4.4 umask
	命令名称:umask
		英文原意:the user file-creation mask   命令所在路径:shell 内置命令
	执行权限:所有用户
	功能描述:显示、设置文件的缺省权限
	语    法:umask [-S]
			 -S 以rwx形式显示新建文件缺省权限 

	范    例:$ umask -S
			 如果单但使用umask 显示0022(第一个0为特殊权限)
			 但是022是经过权限掩码的，真实的权限应为777 - 022 = 755

			 假如我认为默认新建文件的权限应为rwxr-xr-- 754,则777 - 754 = 023
			 使用umask 023 设置默认新建文件权限

## 5. 文件搜索命令

### 5.1 find
	命令名称:find
		英文原意:   命令所在路径:/bin/find
	执行权限:所有用户
	功能描述:文件搜索
	语    法:find [搜索范围] [匹配条件]

	范    例:$ find /etc -name init  (精准搜索，如果查找含"init"的文件可用"*init*"；如果查找"initxxx"的文件可用"init???")
				在目录/etc 中查找文件init (-name 不区分大小写)

			 $ find / -size +204800 (204800是数据块大小，1数据块=512字节=0.5k;100M=102400KB=204800数据块)
			 	+n 大于  -n 小于  n等于

			 $ find /home -user sky
			 	在根目录下查找所有者为sky的文件
			 	-group 根据所属组查找

			 $ find /etc -cmin -5
			 	在/etc 下查找5分钟被修改过属性的文件和目录
			 	-amin 访问时间 access
			 	-cmin 文件属性 change
			 	-mmin 文件内容 modify

			 $ find /etc -size +163840 -a -size -204800
			 	在/etc 下查找大于80MB而小于100MB的文件
			 	-a 两个条件同时满足(and)
			 	-o 两个条件满足任意一个即可(or)

			 $ find /etc -name inittab -exec ls {}\;
			 	在/etc 下查找inittab 文件并显示详细信息
			 	-exec/-ok  命令    {}\     ;    对搜索结果执行操作
			 	(ok会询问) (ls -l) (格式) (结束)

			 -type 根据文件类型查找 (软链接文件)
			 	f 文件  d 目录

			 -inum 根据i节点查找 (通过它来删除对应i节点的文件或查找硬链接)