#Gentoo Install Step#

##安装平台##
* PC: ThinkPad E430c
* Date: 2014-3-5

##开始安装##

###1.下载刻录光盘###

###2.测试网络###

    # ifconfig
    # ping -c 3 www.gentoo.org

###3.磁盘分区###

    /dev/sda1	(swap)	6144M	Swap partition
    /dev/sda2	ext2	128M	Boot partition
    /dev/sda3	ext4	30000M  Root partition
    /dev/sda4	ext4	Rest of the disk	Home partition
    
####创建文件系统####

    # mkfs.ext2 /dev/sda2
    # mkfs.ext4 /dev/sda3
    # mkfs.ext4 /dev/sda4

    # mkswap /dev/sda1
    # swapon /dev/sda1
    
####挂载####

