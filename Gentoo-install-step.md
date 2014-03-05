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

###5.配置编译选项###

    # nano -w /mnt/gentoo/etc/portage/make.conf
---
    CFLAGS="-march=core2 -O2 -pipe"
    CXXFLAGS="${CFLAGS}"
    MAKEOPTS="-j5"
    
Ctrl-X 保存

###6.安装基本系统###

####Chrooting####

#####选择镜像####

    # mirrorselect -i -o >> /mnt/gentoo/etc/portage/make.conf
    # mirrorselect -i -r -o >> /mnt/gentoo/etc/portage/make.conf
    
#####拷贝DNS信息#####

    # cp -L /etc/resolv.conf /mnt/gentoo/etc/
    
#####挂载必要的文件系统#####

    # mount -t proc proc /mnt/gentoo/proc
    # mount --rbind /sys /mnt/gentoo/sys
    # mount --rbind /dev /mnt/gentoo/dev
    
#####进入新环境#####

    # chroot /mnt/gentoo /bin/bash
    # source /etc/profile
    # export PS1="(chroot) $PS1"
    
#####配置Portage#####

    # emerge-webrsync
    # emerge --sync

#####选择需要的环境配置#####
    
    # eselect profile list
    Available profile symlink targets:
      [1]   default/linux/amd64/13.0 *
      [2]   default/linux/amd64/13.0/desktop
      [3]   default/linux/amd64/13.0/desktop/gnome
      [4]   default/linux/amd64/13.0/desktop/kde
---
    # eselect profile set 2

#####配置USE变量#####
    
    # nano -w /etc/portage/make.conf
---
    USE="-gtk -gnome qt4 kde dvd alsa cdr"

#####设置时区#####

    # echo "Europe/Brussels" > /etc/timezone
    # emerge --config sys-libs/timezone-data
    
#####Configure locales#####

    # nano -w /etc/locale.gen
---
    en_US ISO-8859-1
    en_US.UTF-8 UTF-8
    de_DE ISO-8859-1
    de_DE@euro ISO-8859-15
---
    # locale-gen
---
    # eselect locale list
    Available targets for the LANG variable:
      [1] C
      [2] POSIX
      [3] en_US
      [4] en_US.iso88591
      [5] en_US.utf8
      [6] de_DE
      [7] de_DE.iso88591
      [8] de_DE.iso885915
      [9] de_DE.utf8
      [ ] (free form)
---   
    # eselect locale set 9 
---    
    # env-update && source /etc/profile 
    
 ###7.手动配置内核###
 
    # emerge gentoo-sources
    # ls -l /usr/src/linux
    lrwxrwxrwx    1 root   root    12 Oct 13 11:04 /usr/src/linux -> linux-3.4.9
    # cd /usr/src/linux
    # make menuconfig
    
===内核配置===
    
    Processor type and features  --->
       [ ] Machine Check / overheating reporting 
       [ ]   Intel MCE Features
       [ ]   AMD MCE Features
       Processor family (AMD-Opteron/Athlon64)  --->
        ( ) Opteron/Athlon64/Hammer/K8
        ( ) Intel P4 / older Netburst based Xeon
        ( ) Core 2/newer Xeon
        ( ) Intel Atom
        ( ) Generic-x86-64
    Executable file formats / Emulations  --->
        [*] IA32 Emulation
    
    Device Drivers --->
      Generic Driver Options --->
        [*] Maintain a devtmpfs filesystem to mount at /dev
        [ ]   Automount devtmpfs at /dev, after the kernel mounted the rootfs
    
    File systems --->
    (Select one or more of the following options as needed by your system)
      <*> Second extended fs support
      <*> Ext3 journalling file system support
      <*> The Extended 4 (ext4) filesystem
      <*> Reiserfs support
      <*> JFS filesystem support
      <*> XFS filesystem support
      ...
      Pseudo Filesystems --->
        [*] /proc file system support
        [*] Virtual memory file system support (former shm fs)
    
    (Enable GPT partition label support if you used that previously)
    -*- Enable the block layer --->
        ...
        Partition Types --->
        [*] Advanced partition selection
          ...
          [*] EFI GUID Partition support
        
    Device Drivers --->
      [*] HID Devices  --->
        <*>   USB Human Interface Device (full HID) support
        
####编译&安装内核####

    # make && make modules_install 
    # cp arch/x86_64/boot/bzImage /boot/kernel-3.4.9-gentoo
    
###8. Configuring your System###    
    
####fstab####

    # nano -w /etc/fstab
    
    /dev/sda2   /boot        ext2    defaults,noatime     0 2
    /dev/sda3   none         swap    sw                   0 0
    /dev/sda4   /            ext4    noatime              0 1
    
    /dev/cdrom  /mnt/cdrom   auto    noauto,user          0 0
        
####设置网络信息####  

#####主机名#####

    # nano -w /etc/conf.d/hostname
---
    hostname="tux"
    
#####域名#####

    # nano -w /etc/conf.d/net
---
    dns_domain_lo="homenetwork"
        
#####配置网络#####

    # nano -w /etc/conf.d/net
    ---
    config_eth0="192.168.0.2 netmask 255.255.255.0 brd 192.168.0.255"
    routes_eth0="default via 192.168.0.1"
    
 #####开机自启动网卡设置#####
 
    # cd /etc/init.d
    # ln -s net.lo net.eth0
    # rc-update add net.eth0 default
    
 #####密码设置#####
 
    # passwd
    
 #####/etc/conf.d/hwclock#####
 
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    