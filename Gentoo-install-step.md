#Gentoo Install Step#

##安装平台##
* PC: ThinkPad E430c
* Date: 2014-3-5

###1.下载刻录光盘###

###2.测试网络###
    # ifconfig
    # ping -c 3 www.gentoo.org

###3.磁盘分区###

    /dev/sda1	(bootloader)	2M	BIOS boot partition
    /dev/sda2	ext2	128M	Boot partition
    /dev/sda3	(swap)	512M or higher	Swap partition
    /dev/sda4	ext4	Rest of the disk	Root partition
    
    