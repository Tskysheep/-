# 目录

# 一 Linux系统简介
##1. 分区类型
	* 主分区：最多只能4个分区
	* 扩展分区：最多只能一个(主分区+扩展分区最多有4个，不能写入数据，只能包含逻辑分区)
	* 逻辑分区

##2. 格式化(写入文件系统)

##3. 硬件 设备设备文件名

	|设备|设备文件名|
	|----|----|
	|IDE硬盘|/dev/hd[a-d]|
	|SCSI/SATA/USB硬盘|/dev/sd[a-p]|
	|光驱|/dev/cdrom或者/dev/sro|
	|软盘|/dev/fd[0-1]|
	|打印机(25针)|/dev/lp[0-2]|
	|打印机(USB)|/dev/usb/lp[0-15]|
	|鼠标|/dev/mouse|

##4. 挂载(盘符)
	* 必须分区
		+ / (根分区)
		+ swap分区 (交换分区、内存2倍、不超过2GB)
	* 推荐分区
		+ /boot (启动分区 200MB)

##5. 文件系统

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
##1. 安装欢迎界面
	* Install or upgrade an existing system (安装或者升级现有的系统)
	* Install system with basic vido driver (安装过程采用基本显卡驱动)
	* Resume install system (进入系统修复模式)
	* Boot from local drive  (退出安装从硬盘启动)
	* Memory test (存储介质检测)

##2. 软件包选择
	* Desktop (桌面)
	* Minimal Desktop (最小化桌面)
	* Minimal (最小化)
	* Basic Server (基本服务器)
	* Database Server (数据库服务器)
	* Web Server (网页服务器)
	* Virtual Host (虚拟主机)
	* Software development workstation (软件开发工作站)


