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

    # mount /dev/sda3 /mnt/gentoo
    # mkdir /mnt/gentoo/boot
    # mount /dev/sda2 /mnt/gentoo/boot
    # mkdir /mnt/gentoo /mnt/gentoo/home
    # mount /dev/sda4 /mnt/gentoo/home

###4.安装基本系统###

####下载Stage Tarball####

    # cd /mnt/gentoo
    # links http://www.gentoo.org/main/en/mirrors.xml
    
####校验####

####解压Stage Tarball####

    # tar xvjpf stage3-*.tar.bz2

####配置编译选项####

    # nano -w /mnt/gentoo/etc/portage/make.conf
    
    
    