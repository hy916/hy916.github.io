---
title: Linux常用命令大全
top: false
cover: false
toc: true
mathjax: true
summary: 这里记录了一些Linux常用命令
tags:
  - Linux
categories:
  - 命令
abbrlink: 44b30305
date: 2020-11-10 13:31:23
password:
---

### 文件和目录

`cd /home`              进入 '/ home' 目录'
`cd ..`                 返回上一级目录
`cd ../..`              返回上两级目录
`cd`                    进入个人的主目录
`cd ~user1`             进入个人的主目录
`cd -`                  返回上次所在的目录
`pwd`                   显示工作路径
`ls`                    查看目录中的文件
`ls -F`                 查看目录中的文件
`ls -l`                 显示文件和目录的详细资料
`ls -a`                 显示隐藏文件
`ls *[0-9]*`            显示包含数字的文件名和目录名
`tree`                  显示文件和目录由根目录开始的树形结构
`lstree`                显示文件和目录由根目录开始的树形结构
`mkdir dir1`            创建一个叫做 'dir1' 的目录
`mkdir dir1 dir2`       同时创建两个目录
`mkdir -p /tmp/dir1/dir2`       创建一个目录树
`rm -f file1`                   删除一个叫做 'file1' 的文件
`rmdir dir1`                    删除一个叫做 'dir1' 的目录
`rm -rf dir1`                   删除一个叫做 'dir1' 的目录并同时删除其内容
`rm -rf dir1 dir2`              同时删除两个目录及它们的内容
`mv dir1 new_dir`               重命名/移动 一个目录
`cp file1 file2`                复制一个文件
`cp dir/* .`                    复制一个目录下的所有文件到当前工作目录
`cp -a /tmp/dir1 .`             复制一个目录到当前工作目录
`cp -a dir1 dir2`               复制一个目录
`ln -s file1 lnk1`              创建一个指向文件或目录的软链接
`ln file1 lnk1`                 创建一个指向文件或目录的物理链接
`touch -t 0712250000 file1`     修改一个文件或目录的时间戳 - (YYMMDDhhmm)
`iconv -l`                      列出已知的编码

### 系统信息

`arch` 显示机器的处理器架构
`uname -m` 显示机器的处理器架构
`uname -r` 显示正在使用的内核版本
`dmidecode -q` 显示硬件系统部件 - (SMBIOS / DMI)
`hdparm -i /dev/hda` 罗列一个磁盘的架构特性
`hdparm -tT /dev/sda` 在磁盘上执行测试性读取操作
`cat /proc/cpuinfo` 显示CPU info的信息
`cat /proc/interrupts` 显示中断
`cat /proc/meminfo` 校验内存使用
`cat /proc/swaps` 显示哪些swap被使用
`cat /proc/version` 显示内核的版本
`cat /proc/net/dev` 显示网络适配器及统计
`cat /proc/mounts` 显示已加载的文件系统
`lspci -tv` 罗列 PCI 设备
`lsusb -tv` 显示 USB 设备
`date` 显示系统日期
`cal 2007` 显示2007年的日历表
`date 041217002007.00` 设置日期和时间 - 月日时分年.秒
`clock -w` 将时间修改保存到 BIOS

### 关机 (系统的关机、重启等)

`shutdown -h now` 关闭系统
`init 0` 关闭系统
`telinit 0` 关闭系统
`shutdown -h hours:minutes &` 按预定时间关闭系统
`shutdown -c` 取消按预定时间关闭系统
`shutdown -r now` 重启
`reboot` 重启
`logout` 注销

### 磁盘空间

`df -h` 显示已经挂载的分区列表
`ls -lSr |more` 以尺寸大小排列文件和目录
`du -sh dir1 估算目录 'dir1'` 已经使用的磁盘空间
`du -sk * | sort -rn` 以容量大小为依据依次显示文件和目录的大小
`rpm -q -a --qf '%10{SIZE}t%{NAME}n' | sort -k1,1n` 以大小为依据依次显示已安装的rpm包所使用的空间 (fedora, redhat类系统)
`dpkg-query -W -f='${Installed-Size;10}t${Package}n' | sort -k1,1n` 以大小为依据显示已安装的deb包所使用的空间 (ubuntu, debian类系统)

### 文件搜索

`find / -name file1` 从 '/' 开始进入根文件系统搜索文件和目录
`find / -user user1` 搜索属于用户 'user1' 的文件和目录
`find /home/user1 -name \*.bin` 在目录 '/ home/user1' 中搜索带有'.bin' 结尾的文件
`find /usr/bin -type f -atime +100` 搜索在过去100天内未被使用过的执行文件
`find /usr/bin -type f -mtime -10` 搜索在10天内被创建或者修改过的文件
`find / -name \*.rpm -exec chmod 755 '{}' \;` 搜索以 '.rpm' 结尾的文件并定义其权限
`find / -xdev -name \*.rpm` 搜索以 '.rpm' 结尾的文件，忽略光驱、捷盘等可移动设备
`locate \*.ps 寻找以 '.ps'` 结尾的文件 - 先运行 'updatedb' 命令
`whereis halt` 显示一个二进制文件、源码或man的位置
`which halt` 显示一个二进制文件或可执行文件的完整路径

### 挂载一个文件系统

`mount /dev/hda2 /mnt/hda2` 挂载一个叫做hda2的盘 - 确定目录 '/ mnt/hda2' 已经存在
`umount /dev/hda2` 卸载一个叫做hda2的盘 - 先从挂载点 '/ mnt/hda2' 退出
`fuser -km /mnt/hda2` 当设备繁忙时强制卸载
`umount -n /mnt/hda2` 运行卸载操作而不写入 /etc/mtab 文件- 当文件为只读或当磁盘写满时非常有用
`mount /dev/fd0 /mnt/floppy` 挂载一个软盘
`mount /dev/cdrom /mnt/cdrom` 挂载一个cdrom或dvdrom
`mount /dev/hdc /mnt/cdrecorder` 挂载一个cdrw或dvdrom
`mount /dev/hdb /mnt/cdrecorder` 挂载一个cdrw或dvdrom
`mount -o loop file.iso /mnt/cdrom` 挂载一个文件或ISO镜像文件
`mount -t vfat /dev/hda5 /mnt/hda5` 挂载一个Windows FAT32文件系统
`mount /dev/sda1 /mnt/usbdisk` 挂载一个usb 捷盘或闪存设备
`mount -t smbfs -o username=user,password=pass //WinClient/share /mnt/share` 挂载一个windows网络共享

### 用户和群组

`groupadd group_name` 创建一个新用户组
`groupdel group_name` 删除一个用户组
`groupmod -n new_group_name old_group_name` 重命名一个用户组
`useradd -c "Name Surname " -g admin -d /home/user1 -s /bin/bash user1` 创建一个属于 "admin" 用户组的用户
`useradd user1` 创建一个新用户
`userdel -r user1` 删除一个用户 ( '-r' 排除主目录)
`usermod -c "User FTP" -g system -d /ftp/user1 -s /bin/nologin user1` 修改用户属性
`passwd` 修改口令
`passwd user1` 修改一个用户的口令 (只允许root执行)
`chage -E 2005-12-31 user1` 设置用户口令的失效期限
`pwck` 检查 '/etc/passwd' 的文件格式和语法修正以及存在的用户
`grpck` 检查 '/etc/passwd' 的文件格式和语法修正以及存在的群组
`newgrp group_name` 登陆进一个新的群组以改变新创建文件的预设群组

### 文件的权限 -- (使用 "+" 设置权限，使用 "-" 用于取消)

`ls -lh` 显示权限
`ls /tmp | pr -T5 -W$COLUMNS` 将终端划分成5栏显示
`chmod ugo+rwx directory1` 设置目录的所有人(u)、群组(g)以及其他人(o)以读（r ）、写(w)和执行(x)的权限
`chmod go-rwx directory1` 删除群组(g)与其他人(o)对目录的读写执行权限
`chown user1 file1` 改变一个文件的所有人属性
`chown -R user1 directory1` 改变一个目录的所有人属性并同时改变改目录下所有文件的属性
`chgrp group1 file1` 改变文件的群组
`chown user1:group1 file1` 改变一个文件的所有人和群组属性
`find / -perm -u+s` 罗列一个系统中所有使用了SUID控制的文件
`chmod u+s /bin/file1` 设置一个二进制文件的 SUID 位 - 运行该文件的用户也被赋予和所有者同样的权限
`chmod u-s /bin/file1` 禁用一个二进制文件的 SUID位
`chmod g+s /home/public` 设置一个目录的SGID 位 - 类似SUID ，不过这是针对目录的
`chmod g-s /home/public` 禁用一个目录的 SGID 位
`chmod o+t /home/public` 设置一个文件的 STIKY 位 - 只允许合法所有人删除文件
`chmod o-t /home/public` 禁用一个目录的 STIKY 位

### 文件的特殊属性 - 使用 "+" 设置权限，使用 "-" 用于取消

`chattr +a file1` 只允许以追加方式读写文件
`chattr +c file1` 允许这个文件能被内核自动压缩/解压
`chattr +d file1` 在进行文件系统备份时，dump程序将忽略这个文件
`chattr +i file1` 设置成不可变的文件，不能被删除、修改、重命名或者链接
`chattr +s file1` 允许一个文件被安全地删除
`chattr +S file1` 一旦应用程序对这个文件执行了写操作，使系统立刻把修改的结果写到磁盘
`chattr +u file1` 若文件被删除，系统会允许你在以后恢复这个被删除的文件
`lsattr` 显示特殊的属性

### 打包和压缩文件

`bunzip2 file1.bz2` 解压一个叫做 'file1.bz2'的文件
`bzip2 file1` 压缩一个叫做 'file1' 的文件
`gunzip file1.gz` 解压一个叫做 'file1.gz'的文件
`gzip file1` 压缩一个叫做 'file1'的文件
`gzip -9 file1` 最大程度压缩
`rar a file1.rar test_file` 创建一个叫做 'file1.rar' 的包
`rar a file1.rar file1 file2 dir1` 同时压缩 'file1', 'file2' 以及目录 'dir1'
`unrar x file1.rar` 解压rar包
`tar -cvf archive.tar file1` 创建一个非压缩的 tarball
`tar -cvf archive.tar file1 file2 dir1` 创建一个包含了 'file1', 'file2' 以及 'dir1'的档案文件
`tar -tf archive.tar` 显示一个包中的内容
`tar -xvf archive.tar` 释放一个包
`tar -xvf archive.tar -C /tmp` 将压缩包释放到 /tmp目录下
`tar -cvfj archive.tar.bz2 dir1` 创建一个bzip2格式的压缩包
`tar -jxvf archive.tar.bz2` 解压一个bzip2格式的压缩包
`tar -cvfz archive.tar.gz` dir1 创建一个gzip格式的压缩包
`tar -zxvf archive.tar.gz` 解压一个gzip格式的压缩包
`zip file1.zip file1` 创建一个zip格式的压缩包
`zip -r file1.zip file1 file2 dir1` 将几个文件和目录同时压缩成一个zip格式的压缩包
`unzip file1.zip` 解压一个zip格式压缩包

### 查看文件内容

`cat file1` 从第一个字节开始正向查看文件的内容
`tac file1` 从最后一行开始反向查看一个文件的内容
`more file1` 查看一个长文件的内容
`less file1` 类似于 'more' 命令，但是它允许在文件中和正向操作一样的反向操作
`head -2 file1` 查看一个文件的前两行
`tail -2 file1` 查看一个文件的最后两行
`tail -f /var/log/messages` 实时查看被添加到一个文件中的内容

### 文件系统分析

`badblocks -v /dev/hda1` 检查磁盘hda1上的坏磁块
`fsck /dev/hda1` 修复/检查hda1磁盘上linux文件系统的完整性
`fsck.ext2 /dev/hda1` 修复/检查hda1磁盘上ext2文件系统的完整性
`e2fsck /dev/hda1` 修复/检查hda1磁盘上ext2文件系统的完整性
`e2fsck -j /dev/hda1` 修复/检查hda1磁盘上ext3文件系统的完整性
`fsck.ext3 /dev/hda1` 修复/检查hda1磁盘上ext3文件系统的完整性
`fsck.vfat /dev/hda1` 修复/检查hda1磁盘上fat文件系统的完整性
`fsck.msdos /dev/hda1` 修复/检查hda1磁盘上dos文件系统的完整性
`dosfsck /dev/hda1` 修复/检查hda1磁盘上dos文件系统的完整性

### 初始化一个文件系统

`mkfs /dev/hda1` 在hda1分区创建一个文件系统
`mke2fs /dev/hda1` 在hda1分区创建一个linux ext2的文件系统
`mke2fs -j /dev/hda1` 在hda1分区创建一个linux ext3(日志型)的文件系统
`mkfs -t vfat 32 -F /dev/hda1` 创建一个 FAT32 文件系统
`fdformat -n /dev/fd0` 格式化一个软盘
`mkswap /dev/hda3` 创建一个swap文件系统

### 