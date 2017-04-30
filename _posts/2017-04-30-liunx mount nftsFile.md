---
layout: post
title:  "在linux下挂载NTFS的文件系统"
date:   2017-03-30 12:26:11 +0800
categories: emacs
---

# 动机
liunx不能识别NFTS磁盘
# 步骤

```shell
首先必须安装了rpmforge软件库的源
1,yum-y install wget

1、下载rpmforge的rpm文件包 
32位系统
[root@linuxsightlinuxsight]#  wget http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.2-1.el6.rf.i686.rpm

64位系统
[root@linuxsightlinuxsight]#  wget          http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.x86_64.rpm
 
2、安装rpmforge的rpm文件包
 
[root@linuxsight linuxsight]#  rpm -ivhrpmforge-release-0.5.2-1.el6.rf.i686.rpm
 
3、安装ntfs-3g
 
[root@linuxsight linuxsight]# yum install fuse-ntfs-3g
Loaded plugins: fastestmirror,refresh-packagekit
Loading mirror speeds from cachedhostfile
* base: mirrors.ta139.com
* extras: ftp.nara.wide.ad.jp
* rpmforge: apt.sw.be
* updates: mirrors.ta139.com
rpmforge                                                | 1.1 kB     00:00
rpmforge/primary                                         | 1.3MB     01:22
rpmforge                                                             3921/3921
Setting up Install Process
Package fuse-2.8.3-1.el6.i686 alreadyinstalled and latest version
Resolving Dependencies
–> Running transactioncheck
—> Package fuse-ntfs-3g.i6860:2010.10.2-1.el6.rf set to be updated
–> Finished DependencyResolution
 
Dependencies Resolved
 
================================================================================
Package            Arch       Version                     Repository      Size
================================================================================
Installing:
fuse-ntfs-3g       i686       2010.10.2-1.el6.rf          rpmforge       637 k
 
Transaction Summary
================================================================================
Install       1 Package(s)
Upgrade       0 Package(s)
 
Total download size: 637 k
Installed size: 1.4 M
Is this ok [y/N]: y
Downloading Packages:
fuse-ntfs-3g-2010.10.2-1.el6.rf.i686.rpm                 | 637 kB     00:35
Running rpm_check_debug
Running Transaction Test
Transaction Test Succeeded
Running Transaction
Warning: RPMDB altered outside of yum.
Installing     :fuse-ntfs-3g-2010.10.2-1.el6.rf.i686                     1/1
 
Installed:
fuse-ntfs-3g.i686 0:2010.10.2-1.el6.rf
 
Complete!
 
成功后你会发现已经可以挂载NTFS了。

```
