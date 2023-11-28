---
title: 路由器RIP协议实验
date: 2023-11-28 17:06:01
tags: 计算机网络
---

实验九、路由信息协议（RIP）实验

请大家画出如图所示拓扑图（与上次实验一样，这次采用动态路由协议进行配置）

![img](../images/clip_image002-1701162382756-3.jpg)

 

| 名称    | 接口           | IP地址         | 网关      |
| ------- | -------------- | -------------- | --------- |
| Router1 | F0/0           | 192.168.1.1/24 |           |
| F0/1    | 172.1.1.1/24   |                |           |
| Router2 | F0/0           | 172.2.2.1/24   |           |
| F0/1    | 192.168.1.2/24 |                |           |
| PC1     |                | 172.1.1.2/24   | 172.1.1.1 |
| PC2     |                | 172.1.1.3/24   | 172.1.1.1 |
| PC3     |                | 172.2.2.2/24   | 172.2.2.1 |
| PC4     |                | 172.2.2.3/24   | 172.2.2.1 |

 ```bash
 Router1：
 
 基本配置如下：
 
  
 
 Router(config)#router rip
 
 Router(config-router)#version 2
 
 Router(config-router)#no auto-summary //这句话的意思是禁止路由器自动汇总网段的子网掩码,自作聪明的判断网段归属于哪一类地址自动添加子网掩码.只有version2版本才能输入此命令,v1版本没有此功能.大家可以试一下,不加这句话,会自动识别成172.1.0.0,思考为什么
 
  
 
 Router(config-router)#network 172.1.1.0
 
 Router(config-router)#network 192.168.1.0
 ```

```bash
Router2

Router(config)#router rip

Router(config-router)#version 2

Router(config-router)#no auto-summary  

Router(config-router)#network 172.2.2.0

Router(config-router)#network 192.168.1.0
```



上面这两步也可以在图形界面配置，配置完成后分别在两个路由器上查看路由表：

Router1上显示信息如下：

```bash
Router#show ip route

Codes: C - connected, S - static, I - IGRP, R - RIP, M - mobile, B - BGP

​    D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area

​    N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2

​    E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP

​    i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area

​    \* - candidate default, U - per-user static route, o - ODR

​    P - periodic downloaded static route

 

Gateway of last resort is not set

 

   172.1.0.0/24 is subnetted, 1 subnets

C    172.1.1.0 is directly connected, FastEthernet0/1

   172.2.0.0/24 is subnetted, 1 subnets

R    172.2.2.0 [120/1] via 192.168.1.2, 00:00:13, FastEthernet0/0 //R代表通过RIP协议学习到的路由条目管理距离值为120,而静态路由条目的管理距离值为1,如果一个网段同时手工配置了静态路由又自动通过RIP 学到了路由条目,会优先选择网段的静态路由.后面的数字是跳数( 度量值),注意，思科路由器的距离定义和书上的不一致，按书上的定义，这个距离应该是2

C  192.168.1.0/24 is directly connected, FastEthernet0/0

 

注意,如果不在version2下加入no auto-summary,则显示结果是下面这样的: 

172.1.0.0/24 is subnetted, 1 subnets

C  172.1.1.0 is directly connected, FastEthernet0/1

R  172.2.0.0/16 [120/1] via 192.168.1.2, 00:00:10, FastEthernet0/0

C  192.168.1.0/24 is directly connected, FastEthernet0/0
```



 ```bash
 这是Router2上的信息
 
  172.1.0.0/24 is subnetted, 1 subnets
 
 R    172.1.1.0 [120/1] via 192.168.1.1, 00:00:10, FastEthernet0/1
 
    172.2.0.0/24 is subnetted, 1 subnets
 
 C    172.2.2.0 is directly connected, FastEthernet0/0
 
 C  192.168.1.0/24 is directly connected, FastEthernet0/1
 ```



测试一下四个PC是否都能互相ping通。

思考并回答这个实验和上次的静态路由配置有何不同。

 ==这次使用端口的ip，通过rip协议，生成自己的学习路径，自动获取通信==

- **静态路由配置**是手动配置的，管理员需要明确指定网络和下一跳路由器的信息。这种方式适用于小型网络或者需要精确控制路由流量的情况，适用于相对稳定的网络环境，其中网络拓扑变化不频繁。
- **RIP协议**是一种动态路由协议，它允许路由器之间交换路由信息，并根据网络拓扑和跳数等信息动态更新路由表。这种方式适用于较大规模的网络，可以自动适应网络拓扑的变化，适用于需要自适应网络拓扑变化的环境，可以更快地适应网络变化。

**请大家截屏记录实验结果，提交报告实验9。**

![img](../images/clip_image004-1701162382756-2.jpg)

![img](../images/clip_image006-1701162382755-1.jpg)

![img](../images/clip_image008-1701162382756-4.jpg)
