---
title: Windows Server 2008系统技巧
author: Feng
type: post
published: 2012-03-14T02:01:29+00:00
url: /my/21.html
hera_post_view:
  - 4
categories:
  - 生活随笔

---
**一、配置Windows Server 2008，以使它更符合您的使用习惯**  
1.安装桌面  
由于是服务器系统，默认是没有华丽的效果的。开启方法如下：  
“开始”→“服务器管理”→“Server Manager”  
在左边一栏找到与“features”有关的项(然后点击Add features);滑动找到desktop experience(中文版叫桌面体验，当然如果是无线使用笔记本的话，无线功能也要加上)，最后重启。  
2.开启Aero  
要开启Aero效果需要启动相关服务。“开始”运行(或者同时按住Win+R键)services.Msc找到Themes右键开启服务。然后右键属性，把启动方式改为自动。  
3.关闭IE SEC  
服务器系统要求很高的安全性，所以微软给IE添加了安全增强。这就使得IE在Internet区域的安全级别一直是最高的，而且无法进行整体调整。  
点击快速运行栏的“服务器管理器”，开启服务器管理器。  
a.勾选“登录时不要显示此控制台”  
b.点击“配置IE ESC”，将对“管理员”和“用户”设置为“禁用”。  
4.去掉关机事件跟踪  
每次关机都要求给出原因，用起来很烦人。去掉的方法不难。  
“开始”“运行”键入gpedit.Msc  
依次打开计算机配置→Windows配置→安全设置→本地策略→安全选项→交互式登录：无须按ctrl+alt+del→勾选“已启用”  
配置Windows Server 2008(2)  
5.让计算机直登录而无须按ctrl+alt+del  
在运行框中键入“gpedit.msc”进入主策略编辑器。1.依次双击：计算机配置→Windows配置→安全设置→本地策略→安全选项→交互式登录：无须按ctrl+alt+del→勾选“已启用”  
6.开启硬件加速  
桌面上右键“个性化”→“显示设置”→“高级设置”  
“疑难解答”→“更改设置”把硬件加速滑到最大就行了  
7.优化前台程序运行如果不想在浏览网页开启多任务，听着音乐的时候感觉到卡，需要把性能优先到前台程序上来。  
打开“高级系统设置”→“高级”→“性能”  
8.优先程序“而非”后台服务  
数据执行保护→仅为基本Windows程序和服务启用“ DEP”  
对注册表进行优化：  
1.提高Win2008系统关机速度。  
定位注册表到HKEY\_CURRENT\_USERControl PanelDesktop ，设置键值WaitToKillAppTimeout为1  
定位注册表到HKEY\_LOCAL\_MACHINESYSTEMCurrentControlSetControl ，设置键值WaitToKillServiceTimeout为1  
2.加快Win2008菜单显示速度  
定位注册表到HKEY\_CURRENT\_USERControl PanelDesktop ，设置键值MenuShowDelay为 1  
3.自动释放Dll占用内存  
定位注册表到HKEY\_LOCAL\_MACHINESOFTWAREMicrosoftWindowsCurrentVersionExplorer ，设置键值AlwaysUnloadDLL为1  
4.加速关闭没有响应的程序  
定位注册表到HKEY\_CURRENT\_USERControl PanelDesktop ，设置键值AutoEndTasks为1  
开始→运行→输入“msconfig”确定→  
(1)启动→点击[全部禁用]→[确定]后，不要重新启动  
(2)服务→勾上“隐藏所有Microsoft服务”的勾→点击[全部禁用]，[应用]→再去掉“隐藏所有Microsoft服务”的勾→将下列服务  
wireless zero configuration，task scheduler，Fast user switching compatibility，Netmeeting remote desktop sharing，terminal services，automatic updates，remote registry，removable storage，  
Indexing service，messenger，server，Computer browser，Print Spooler  
前的勾去掉(请仔细查找，大小写忽略。依安装版本和功能的不同，有的服务可能没有。电脑若在局域网内，用时将server，Computer browser手动打开;若有打印机，用时将Print Spooler手动打开)[确定]后，重新启动。  
经过以上终极优化设置，Windows server 2008性能、稳定性、易用性以及外观，都将达到一个比较完美的档次。