# Linux

## 基础知识

### 目录结构

- /dev  存放抽象硬件
- /lib  存放系统库文件
- /sbin  存放特权级二进制文件
- /var  存放变量文件
- /home  普通用户目录
- /etc 存放配置文件目录
- /boot  存放内核与启动文件
- /bin  存放二进制文件（可执行命令）
- /usr  存放安装程序（软件默认目录）
- /mnt 文件挂载目录（U盘、光驱）
- /root  特权用户目录
- /opt  大型软件存放目录（非强制）

### 重要配置文件

```
/etc/
/etc/sysconfig/network-script/ifcfg-[网卡名称] : 网卡配置文件
/etc/resolv.conf : DNS客户端配置文件
/etc/fstab : 配置开机设备自动挂载的文件
/etc/rc.local : 存放开机自启动程序命令的文件
/etc/inittab : 系统启动设定运行级别等配置的文件
/etc/profile : 配置系统环境变量的文件
/etc/bashrc : 配置别名的文件
/etc/profile.d : 用户登录后执行的脚本所在目录
/etc/init.d ： 软件启动程序所在的目录(centos 6)
/usr/lib/systemd/system ： 软件启动程序所在的目录(centos 7)
/etc/hostname : 主机名文件
/etc/hosts : 系统本地DNS解析文件
/etc/motd : 用户登录系统问候文本文件
/etc/os-relaease : 系统版本信息
/etc/sysctl.conf : Linux内核参数设置文件
```

```
/proc/
/proc/meminfo : 系统内存信息
/proc/cpuinfo : 系统处理器的信息
/proc/loadavg : 系统负载信息，uptime的结果
/proc/mounts : 已加载的文件系统的列表
```

```
/var/
/var/log : 系统及软件运行信息文件日志目录
/var/log/messages : 系统级别日志文件
/var/log/secure : 用户登录信息日志文件
/var/log/dmesg : 记录硬件信息加载清空的日志文件
```

## 基础命令

### tip : options简写

```
options可以简写
例如: ls -h -a  === ls-ah
```

### cd

change directory（更改目录）

```
cd [目录]

特殊目录:
.   : 当前工作目录
..  : 上一级的工作目录
-   : 上一次的工作目录
~   : 当前系统登录的用户home目录
```

### ls

list（列表）

列出文件夹中的内容

```
ls [option] [目录文件夹]

options:
-a   ：列出所有文件以及信息，包括隐藏文件
-l   : 详细列出文件夹中的内容
-h   : 列出文件信息，但是文件大小有单位
--full-time  : 以完整的时间格式列出信息
-t   : 根据最后修改时间排序列出的文件（降序）

-F   : 在列出的文件结尾标记特殊符号
	/ 结尾为文件夹
	* 结尾为可执行文件
	@ 结尾为软连接（快捷方式）
	结尾为空则为普通文件类型
	
-d   : 显示当前所在文件夹的信息，不会列出文件
-r   : reverse 逆转排序
-S   : 针对文件大小进行排序（降序）
-i   : 显示出文件的inode信息
```

### pwd

print work directory（打印工作目录）

输出当前所处的工作目录的绝对路径

```
pwd
```

### mkdir

make directory（创建目录）

```
mkdir [options] [目录]

options:
-p	 : 递归创建目录，会逐层创建目录

目录：
{目录1,目录2,...,目录n}	 : 同时创建多个平级目录
例如: mkdir {dirBz,dirZz}

目录名称{序号..序号}	 ： bash脚本创建多个平级目录
序号:阿拉伯数字、大小写字母
例如: mkdir dir{1..3}
	 mkdir dir{a..z}
	 mkdir dir{A..Z}
```







### su

switch user（切换用户）

```
su - [用户名]   : 完全的环境变量用户切换
```



### logout

login out（登出）

退出当前系统用户

```
logout
```

