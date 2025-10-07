---
title: Linux云主机（VPS）HOME分区扩容操作流程（来自：西部数码）
author: Feng
type: post
published: 2014-02-24T13:22:01+00:00
url: /it/73.html
hera_post_view:
  - 2
categories:
  - IT网络

---
以下是linux服务器增加home分区的操作流程，VPS或云主机升级后需要增加home分区大小的，可以按此方法增加。**特别提醒：删除分区后一定要先建立分区再保存，删除后点了保存会导致数据丢失，如果对****linux****不熟悉的，建议提交维护工单我司手工处理，费用30****元。**该操作有风险，为避免误操作导致数据丢失，操作前请对您的重要数据进行备份！****  
&nbsp;  
**提示：**  
&nbsp;  
灰色内容为linux系统显示  
红色内容为输入的命令  
//绿色内容为命令或显示内容说明  
&nbsp;  
&nbsp;  
&nbsp;  
[root@west5066 ~]# df -vh    //查看home分区所在的硬盘名称，我司一般是sdb  
文件系统              容量  已用可用已用% 挂载点  
/dev/sda1             9.7G  2.6G  6.7G  28% /  
tmpfs                 252M     0  252M   0% /dev/shm  
/dev/sdb1             9.9G  172M  9.2G   2% /home  
[root@west5066 ~]#service httpd stop //使用nginx的结束nginxd  
[root@west5066 ~]#service wdapache stop  
[root@west5066 ~]#service mysqld stop  
[root@west5066 ~]#fuser -m /home -k   //以上命令是停止服务  
[root@west5066 ~]#umount /home      //取消/home挂载  
[root@west5066 ~]#parted /dev/sdb    //输入parted /dev/sdb 这里是磁盘名,如果没有这个程序执行yum install parted 安装！  
GNU Parted 2.1  
使用 /dev/sdb  
Welcome to GNU Parted! Type &#8216;help&#8217; to view a list of commands.  
(parted) print  
Model: Virtio Block Device (virtblk)  
Disk /dev/sdb: 20GB                                       //记录磁盘总大小  
Sector size (logical/physical): 512B/512B  
Partition Table: msdos  
Number  Start   End    Size   Type     File system  标志  
1      1049kB  9.9G  9.9G  primary  ext4          //记录Start 大小  
(parted) rm 1  
&nbsp;  
(parted) mkpart  
分区类型?  primary/主分区/extended/扩展分区? p  
文件系统类型?  [ext2]?       //直接回车  
<span style="color: #808080; font-family: Calibri;">起始点? </span>1049kB             //刚才记录的Start大小  
<span style="color: #808080; font-family: Calibri;">结束点? </span><span style="color: #ff0000; font-family: Calibri;">20GB            </span><span style="color: #00b050; font-family: Calibri;">//刚才记录的磁盘总大小<br /> </span><span style="color: #808080;">(parted) </span><span style="color: #ff0000;">quit<br /> </span>信息: You may need to update /etc/fstab.  
[root@west5066 ~]# resize2fs -f /dev/sdb1   //输入resize2fs -f /dev/sdb1，这里是分区名，如果提示fsck，请执行后再操作resize2fs  
resize2fs 1.39 (29-May-2006)  
Filesystem at /dev/sdb1 is mounted on /home; on-line resizing required  
Performing an on-line resize of /dev/sdb1 to 5242852 (4k) blocks.  
The filesystem on /dev/sdb1 is now 5242852 blocks long.  
[root@west5066 ~]#mount -a //挂载分区  
[root@west5066 ~]# df -vh    //再用df –lh 查询下home分区大小，可以看到已经增加了。  
文件系统              容量  已用可用已用% 挂载点  
/dev/sda1             9.7G  2.6G  6.7G  28% /  
tmpfs                 252M     0  252M   0% /dev/shm  
/dev/sdb1              20G  177M   19G   1% /home  
[root@west5066 ~]#service mysqld start  
[root@west5066 ~]#service httpd start         //使用nginx的启动nginxd  
[root@west5066 ~]#service wdapache start            //启动服务

<div>
</div>

<div>
  以下是linux服务器增加home分区的操作流程，VPS或云主机升级后需要增加home分区大小的，可以按此方法增加。<strong>特别提醒：删除分区后一定要先建立分区再保存，删除后点了保存会导致数据丢失，如果对</strong><strong>linux</strong><strong>不熟悉的，建议提交维护工单我司手工处理，费用30</strong><strong>元。<strong>该操作有风险，为避免误操作导致数据丢失，操作前请对您的重要数据进行备份！</strong></strong><br /> &nbsp;<br /> <strong>提示：</strong><br /> &nbsp;<br /> 灰色内容为linux系统显示<br /> 红色内容为输入的命令<br /> //绿色内容为命令或显示内容说明<br /> &nbsp;<br /> &nbsp;<br /> &nbsp;<br /> [root@west5066 ~]# df -vh    //查看home分区所在的硬盘名称，我司一般是sdb<br /> 文件系统              容量  已用可用已用% 挂载点<br /> /dev/sda1             9.7G  2.6G  6.7G  28% /<br /> tmpfs                 252M     0  252M   0% /dev/shm<br /> /dev/sdb1             9.9G  172M  9.2G   2% /home<br /> [root@west5066 ~]#service httpd stop //使用nginx的结束nginxd<br /> [root@west5066 ~]#service wdapache stop<br /> [root@west5066 ~]#service mysqld stop<br /> [root@west5066 ~]#fuser -m /home -k   //以上命令是停止服务<br /> [root@west5066 ~]#umount /home      //取消/home挂载<br /> [root@west5066 ~]#parted /dev/sdb    //输入parted /dev/sdb 这里是磁盘名,如果没有这个程序执行yum install parted 安装！<br /> GNU Parted 2.1<br /> 使用 /dev/sdb<br /> Welcome to GNU Parted! Type &#8216;help&#8217; to view a list of commands.<br /> (parted) print<br /> Model: Virtio Block Device (virtblk)<br /> Disk /dev/sdb: 20GB                                       //记录磁盘总大小<br /> Sector size (logical/physical): 512B/512B<br /> Partition Table: msdos<br /> Number  Start   End    Size   Type     File system  标志<br /> 1      1049kB  9.9G  9.9G  primary  ext4          //记录Start 大小<br /> (parted) rm 1<br /> &nbsp;<br /> (parted) mkpart<br /> 分区类型?  primary/主分区/extended/扩展分区? p<br /> 文件系统类型?  [ext2]?       //直接回车<br /> <span style="color: #808080; font-family: Calibri;">起始点? </span>1049kB             //刚才记录的Start大小<br /> <span style="color: #808080; font-family: Calibri;">结束点? </span><span style="color: #ff0000; font-family: Calibri;">20GB            </span><span style="color: #00b050; font-family: Calibri;">//刚才记录的磁盘总大小<br /> </span><span style="color: #808080;">(parted) </span><span style="color: #ff0000;">quit<br /> </span>信息: You may need to update /etc/fstab.<br /> [root@west5066 ~]# resize2fs -f /dev/sdb1   //输入resize2fs -f /dev/sdb1，这里是分区名，如果提示fsck，请执行后再操作resize2fs<br /> resize2fs 1.39 (29-May-2006)<br /> Filesystem at /dev/sdb1 is mounted on /home; on-line resizing required<br /> Performing an on-line resize of /dev/sdb1 to 5242852 (4k) blocks.<br /> The filesystem on /dev/sdb1 is now 5242852 blocks long.<br /> [root@west5066 ~]#mount -a //挂载分区<br /> [root@west5066 ~]# df -vh    //再用df –lh 查询下home分区大小，可以看到已经增加了。<br /> 文件系统              容量  已用可用已用% 挂载点<br /> /dev/sda1             9.7G  2.6G  6.7G  28% /<br /> tmpfs                 252M     0  252M   0% /dev/shm<br /> /dev/sdb1              20G  177M   19G   1% /home<br /> [root@west5066 ~]#service mysqld start<br /> [root@west5066 ~]#service httpd start         //使用nginx的启动nginxd<br /> [root@west5066 ~]#service wdapache start            //启动服务</p> 
  
  <div>
  </div>
  
  <div>
  </div>
</div>