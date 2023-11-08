---
title: 计算机网络cisco交换机基本配置
date: 2023-11-07 14:16:57
tags: 计算机网络
---

# 实验四 交换机的基本配置

### 一、实验目的


1.了解交换机的作用。

2.掌握交换机的基本配置方法。

3.熟悉Cisco Packet Tracer的使用。

### 二、实验内容

1．以星型结构为例，练习使用Cisco Packet Tracer画出网络拓扑图。

2．掌握交换机的基本配置模式，练习交换机的基本配置命令。

### 三、实验原理

1．交换机的基本配置模式：

常见的配置模式有：用户模式、特权模式、全局配置模式、接口配置模式、VLAN配置模式和访问配置模式。

**用户模式**：switch>   一旦与交换机建立连接，就进入了用户模式。在这种模式下，只能查看网络设备的运行状态和简单的统计信息。

**特权模式**：Switch#   在该模式下可为交换机设置账号和密码。

进入方法：在默认的用户模式下输入：enable 进入。

退出方法：输：exit 退回到用户模式。

注意用户模式和特权模式的前面代码的区别：一个是switch>；一个是Switch#。

**全局配置模式**：(config)#   在该模式下可对交换机的全局参数进行配置。

进入方法：在特权模式下，使用命令“configure terminal（或者简写成conf t）”

**接口配置模式**：(config-if)#   在该模式下，仅对该接口的参数进行配置

进入方法：在全局配置模式下，使用命令“interface 接口名

**VLAN配置模式**：(config-vlan)#

进入方法：在全局配置模式下输入 vlan database 进入

**访问配置模式：**(config-line)#

进入方法：在全局配置模式下输入line vty 线路编号 进入

 

备注：

1）在任何模式下，用户在输入命令时，不用全部将其输入，只要前几个字母能够唯一标识该命令即可，此时按Tab键将显示全称。

如：interface serial 0/1可以写成：int s0/1

2）在任何模式下，输入一个“？”即可显示所有在该模式下的命令。

3）如果不会拼写某个命令，可以键入开始的几个字母，在其后紧跟一个“？”，交换机即显示有什么样的命令与其匹配。

4）如果不知道命令后面的参数应该是什么，可以在该命令的关键字后加一个空格，键入“？”，交换机即会提示与“？”对应的参数是什么，例如：Switch#show ？

5）要删除某条配置命令，可在原配置命令前加一个no和空格。

6）退回上一层模式用“exit”，退回到特权模式用“end”

7）查看交换机配置文件信息用==show startup-config==，查看当前所有配置信息用==show running-config==。保存当前配置用==copy running-config startup-config==（若没保存，重启后配置丢失）。重启交换机用reload命令。这些命令需要在特权模式下输入。

 

2．配置交换机(网管型交换机)，首先要把交换机和电脑连接，连接方法是用专门的Console线连接交换机的Console端口和计算机的COM口。现在电脑如果没有COM口，用RS232转USB数据线即可。

可进行网络管理的交换机上一般都有一个“Console”端口，它是专门用于对交换机进行配置和管理的。通过Console端口连接并配置交换机，是配置和管理交换机必须经过的步骤。因为其他方式的配置往往需要借助于IP地址、域名或设备名称才可以实现，而新购买的交换机显然不可能内置有这些参数，所以Console端口是最常用、最基本的交换机管理和配置端口。

Console线也分为两种，一种是串行线，即两端均为串行接口(两端均为母头或一端为公头，另一端为母头)，两端可以分别插入至计算机的串口和交换机的Console端口;另一种是两端均为RJ-45接头(RJ-45-to-RJ-45)的扁平线。

硬件连接好了，就要进行软件配置，安装Console数据线的驱动，并使用系统自带的仿真终端软件，设置好波特率、数据位等信息后，通过交换机的出厂默认用户名和密码就可以登陆交换机。

 

### 四、实验步骤

在模拟器中构建一个如下图所示的网络拓扑图，PC0和PC1使用直通线与交换就的f0/1口和f0/2口相连，PC3使用RS232接口通过Console线缆与交换机的Console接口连接。配置每个PC的IP地址如下图所示，子网掩码都为255.255.255.0。

![说明: C:\Users\LZ\AppData\Local\Temp\1603173757(1).png](../images/clip_image002.gif)

1）连接到交换机

对交换机的第一次配置，要在PC3的配置窗口的Desktop选项卡下，选择Terminal，打开下图所示对话框，

![说明: C:\Users\LZ\AppData\Local\Temp\1603174148(1).png](../images/clip_image004.gif)

按下OK键开始进入交换机的配置。

也可以直接单击交换机，点击CLI标签进行配置。

请输入以下命令，思考并练习。

2）修改交换机的名称

```shell
Switch>                         用户模式

Switch>enable                      enable进入特权模式

Switch#config terminal                   进入全局配置模式

Switch(config)#hostname SW                设置交换机名称为SW
```

 

3）设置口令

```shell
SW(config)#enable password cisco              设置使能口令cisco

SW(config)#enable secret cisco1                设置使能密码cisco1

SW(config)#line vty 0 4             开启5个vty会话线路，线路编号为0-4

SW(config-line)#password ptxy         设置远程登录密码

SW(config-line)#login             设置在远程登录时用密码验证

SW(config-line)#end              保存并退出
```

注：enable password在交换机的配置文件中以明文形式存储；而enable secret以密文形式存储如果同时设置两个口令，则只有enable secret有效，为了安全起见，通常只配置enable secret。

当需要远程登录（如TELNET）管理交换机时，必须有line vty 0 4开始的这三行命令，line vty 0 4表示开启0-4共5条远程终端会话线路，password ptxy设置远程登录密码，login这里如果写成no login，则远程登录时不需要密码。

 

4）配置交换机的管理IP地址和默认网关

交换机完成首次配置后，后期可能需要通过TELNET等方式对其进行远程管理，这时就需要设置交换机的IP地址和默认网关等管理信息，具体命令如下：

```shell
SW>en

Password:                  输入前面设置的使能密码cisco1

SW#conf t

SW(config)#interface vlan1           进入VLAN1虚拟接口配置模式

SW(config-if)#ip address 192.168.1.8 255.255.255.0    设置交换机的IP地址与子网掩码

SW(config-if)#no shutdown              激活该接口

SW(config-if)#exit                  返回到上一层模式

SW(config)#ip default-gateway 192.168.1.8        设置交换机默认网关

SW(config)#end

SW#
```



此时，在PC0或PC1的配置窗口的Desktop选项卡下，打开Command Prompt窗口，输入命令telnet 192.168.1.8，当提示要输密码时，输入前面设置的远程登录密码就成功连接到了交换机。

 

### 五、实验报告要求

1．练习使用Cisco Packet Tracer 画出网络拓扑结构图，掌握交换机的基本配置模式，练习交换机的基本配置命令，并截屏+文字记录相关步骤。提交word文档，文件名为：学号姓名实验四。先不交，与后续交换机实验报告一起交。

![image-20231107142742550](../images/image-20231107142742550.png)

 ![image-20231107142901504](../images/image-20231107142901504.png)

```shell
version 12.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname SW
!
enable secret 5 $1$mERr$q.MA2tj.WFptzvbifq/1i.
enable password cisco
!
!
spanning-tree mode pvst
!
interface FastEthernet0/1
!
interface FastEthernet0/2
!
interface FastEthernet0/3
!
interface FastEthernet0/4
!
interface FastEthernet0/5
!
interface FastEthernet0/6
!
interface FastEthernet0/7
!
interface FastEthernet0/8
!
interface FastEthernet0/9
!
interface FastEthernet0/10
!
interface FastEthernet0/11
!
interface FastEthernet0/12
!
interface FastEthernet0/13
!
interface FastEthernet0/14
!
interface FastEthernet0/15
!
interface FastEthernet0/16
!
interface FastEthernet0/17
!
interface FastEthernet0/18
!
interface FastEthernet0/19
!
interface FastEthernet0/20
!
interface FastEthernet0/21
!
interface FastEthernet0/22
!
interface FastEthernet0/23
!
interface FastEthernet0/24
!
interface Vlan1
 no ip address
 shutdown
!
!
line con 0
!
line vty 0 4
 password ptxy
 login
line vty 5 15
 login
!
!
```

```
version 12.1: 这一行指定了配置文件所使用的Cisco IOS软件的版本。

no service timestamps log datetime msec 和 no service timestamps debug datetime msec: 这两行命令禁用了日志和调试信息中的时间戳，并且不包括毫秒级别的时间信息。这可以使日志文件更加简洁。

no service password-encryption: 这一行命令禁用了密码加密。通常情况下，Cisco设备会对配置中的密码进行加密存储，但这个命令会取消加密，以便在配置文件中明文显示密码。

hostname SW: 这一行命令设置了设备的主机名为 "SW"，这是设备的标识符。

enable secret 5 $1$mERr$q.MA2tj.WFptzvbifq/1i.: 这一行设置了特权模式的密码，这是用于访问设备特权模式的密码。密码是加密的，以提高安全性。密码的实际值是 "
1
1mERr$q.MA2tj.WFptzvbifq/1i."。

enable password cisco: 这一行设置了备用的特权模式密码，如果启用密码被忘记，可以使用这个密码来访问特权模式。不像前面的密码，这个密码以明文形式存储在配置中。

spanning-tree mode pvst: 这一行命令配置了Spanning Tree Protocol (STP) 的模式为Per-VLAN Spanning Tree (PVST)。PVST是Cisco的STP实现，允许每个VLAN都有自己的STP实例，以提高网络的冗余性和可靠性。

接口配置部分: 这一部分包括了多个FastEthernet接口（FastEthernet0/1 到 FastEthernet0/24）。在这个示例中，这些接口没有配置IP地址或其他参数，因此它们可能是未配置的接口或者处于交换机模式。

interface Vlan1: 这一行配置了VLAN 1 接口，但没有分配IP地址，并将接口关闭（shutdown）。通常情况下，VLAN 1 用于管理目的，但在这个配置中，它被禁用了。

line con 0 和 line vty 0 4 配置了控制台和虚拟终端（Telnet或SSH）的访问。它们分别设置了密码（控制台密码为 "ptxy"）和允许登录。

line vty 5 15 配置了更多的虚拟终端线路，允许更多的远程Telnet或SSH会话。
```



最后在交换机这里进行配置，让他可以被远程的telnet

![image-20231107144113020](../images/image-20231107144113020.png)
