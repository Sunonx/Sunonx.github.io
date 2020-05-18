# Routing Exange Review


## 前言
**基本概述**：

-指导教师：刘云生

- 学习时间：2020.3.14-2020.5.20
- 教学内容：CCNA  CCNP
- 考核内容：教材，CCNA题库(640-802)
- 考核题型：选择、填空、简答、综合配置
- 考试时间：2020.8.8---&
- 参考教材：

&emsp;&emsp;-《路由交换技术》 清华大学出版社 吴建胜等

&emsp;&emsp;-《TCP/IP路由技术》 人民邮电出版社  葛健立等

&emsp;&emsp;-《 TCP/IP详解》

## C0 review
###### OSI模型
- 7.应用层

应用层（Application Layer）提供为应用软件而设的接口，以设置与另一应用软件之间的通信。例如: HTTP、HTTPS、FTP、TELNET、SSH、SMTP、POP3、HTML等。

- 6.表达层

表达层（Presentation Layer）把数据转换为能与接收者的系统格式兼容并适合传输的格式。

- 5.会话层

会话层（Session Layer）负责在数据传输中设置和维护计算机网络中两台计算机之间的通信连接。

- 4.传输层

传输层（Transport Layer）把传输表头（TH）加至数据以形成数据包。传输表头包含了所使用的协议等发送信息。例如:传输控制协议（TCP）等。

- 3.网络层

网络层（Network Layer）决定数据的路径选择和转寄，将网络表头（NH）加至数据包，以形成报文。网络表头包含了网络数据。例如:互联网协议（IP）等。

- 2.数据链路层

数据链路层（Data Link Layer）负责网络寻址、错误侦测和改错。当表头和表尾被加至数据包时，会形成信息框（Data Frame）。数据链表头（DLH）是包含了物理地址和错误侦测及改错的方法。数据链表尾（DLT）是一串指示数据包末端的字符串。例如以太网、无线局域网（Wi-Fi）和通用分组无线服务（GPRS）等。

分为两个子层：逻辑链路控制（logical link control，LLC）子层和介质访问控制（Media access control，MAC）子层。

- 1.物理层

物理层（Physical Layer）在局部局域网上传送数据帧（Data Frame），它负责管理电脑通信设备和网络媒体之间的互通。包括了针脚、电压、线缆规范、集线器、中继器、网卡、主机接口卡等。

[改定义来自维基百科](https://zh.wikipedia.org/wiki/OSI%E6%A8%A1%E5%9E%8B)

###### 封装和解封装

**封装 （ encapsulate/encapsulation）**：数据要通过网络进行传输，要从高层一层一层的向下传送，如果一个主机要传送数据到别的主机，先把数据装到一个特殊协议报头中，这个过程叫-----封装
- 封装分为：切片和加控制信息

**解封装**：上述的逆向过程

![router01.png](https://raw.githubusercontent.com/Sunonx/Sunonx.github.io/master/images/router01.png)

![router02.png](https://raw.githubusercontent.com/Sunonx/Sunonx.github.io/master/images/router02.png)
![router03.png](https://raw.githubusercontent.com/Sunonx/Sunonx.github.io/master/images/router03.png)

###### 子网划分

[参考之前写的文章vlan的划分](https://sunon.xyz/vlan/)

**VLSM（Variable Length Subnet Mask，可变长子网掩码）**:

- 规定了如何在一个进行了子网划分的网络中的不同部分使用不同的子网掩码。这对于网络内部不同网段需要不同大小子网的情形来说很有效。

- VLSM其实就是相对于类的IP地址来说的。A类的第一段是网络号（前八位），B类地址的前两段是网络号（前十六位），C类的前三段是网络号（前二十四位）。而VLSM的作用就是在类的IP地址的基础上，从它们的主机号部分借出相应的位数来做网络号，也就是增加网络号的位数。各类网络可以用来再划分子网的位数为：A类有二十四位可以借，B类有十六位可以借，C类有八位可以借（可以再划分的位数就是主机号的位数。实际上不可以都借出来，因为IP地址中必须要有主机号的部分，而且主机号部分剩下一位是没有意义的，所以在实际中可以借的位数是在上面那些数字中再减去2，借的位作为子网部分）。

## C1 IOS配置基础

###### Cisco设备上常见和常用的接口：
- ONSOLE接口（控制台接口）

- AUX接口（辅助接口）

- ETHERNET接口（以太网接口）

- SERIAL接口（串行接口）

  **主要有以下作用**： 

  - 远程拨号调试。

  - 拨号备份。

  - 网络设备之间的线路连接。

  - 本地调试口。

###### RAM

- RAM保存系统当前的配置，并保存IOS的运行版本 

- RAM保存路由表，执行包缓冲，对因超载而不能直接输出的包进行排队。

- RAM可缓存ARP协议中地址映射的信息。

- 当路由器断电后，RAM的内容就丢失。

###### 闪存

- 闪存用于保留操作系统和路由器微代码映像。

- 闪存也可用于通过tftp协议传送操作系统映像到另一个路由器。

- 闪存可存放路由器配置文件的备份。

- 路由器断电时，闪存中的信息不会丢失。

###### IOS配置过程

- 通过CONSOLE接口直接配置

- 通过AUX接口进行远程配置

- 通过TELNET进行远程配置

- 通过TFTP服务器进行远程配置

- 通过WEB或者SNMP网管工作站远程配置

###### IOS配置命令
1. 启用**加密口令（enable secret password）**和**启用口令（enable password）**    

   - 启用加密口令在配置系统时是加密过的并且不可见；

   - 启用口令在纯文本情况下就可以显示出来。

   - 如果两个口令都是设置的话，启用加密口令总是优先使用。

   :loudspeaker:在安装模式中，IOS要求这两个口令必须存在**差别**。

2. router模式

   - 用户模式`Router>`

   - 特权模式`Router#`

   - 全局配置模式`Router(config)#`

   - 接口配置模式：`Router(config-if)#`   
        
   - 子接口配置模式：`Router(config)#interface fa0/0.1` //进入子接口
                      
     - 子接口状态:`Router(config-subif)#` 
        
   - Line模式：`Router(config-line)#`      
        
   - 路由模式：`Router(config-router)#`    

3. 路由协议配置命令
   `router protocol [parameter]`

     protocol:路由协议的总类   &emsp;parameter：路由协议的参数

   ```
    Router(config)#router rip          //配置rip协议
    Router(config-router)# 

    Router(config)#router igrp 100     //配置igrp协议
    Router(config-router)# 

    Router(config)#router ospf 1       //配置ospf协议
    Router(config-router)# 

   ```

4. show命令集
   
    Switch#show `version`            //显示IOS版本信息

    Switch#show `int vlan 1 brief`  //简单的显示VLAN1的信息

    Switch#show `running-config`    //显示正在运行的配置文件

    Switch#show `startup-config`     //显示己经保存的配置文件

    Switch#show `mac-address-table`  //显示MAC地址表

    Switch#show `mac-address-table`   //显示MAC地址表更新的间隔，默认为5分钟

    Switch#show `neighbor detail`     //显示邻居详细信息

    Switch#show `traffic`             //显示CDP流量
    
    Switch#show `?`

5. 设置交换机的网关和DNS名称服务器的IP地址
   
    Swith(config)# `ip default-gateway` 192.168.10.8//交换机的网关设置为192.168.10.8

    Swith(config)#`ip domain -name server` 202.106.0.20 //设置DNS名称服务器地址

    Swith(config)# no ip domain-lookup   //交换机名称服务器的域名查询

6. 创建、删除、查看VLAN
   
    Switch#`vlan database`       //进入vlan数据库配置模式

    Switch(vlan)#`vlan 2`        //创建VLAN2命名为vlan &emsp;2

    Switch(vlan)#exit                 //退出时应用生效

    Swith(vlan)#no vlan 2               //删除vlan2

    Switch(config)# interface f0/1

    Switch(config-if)# `switchport access vlan 2`      //将端口加入vlan 2中

    Switch(config-if)# no switchport access vlan 2   //将端口从vlan2中删除

    Switch(config)# `interface range f0/1–10`    // 进行F0/1到10端口范围

    Switch(config-if-range)# switchport access vlan 2  //将f0/1到f0/10之间的所有端口加入vlan 2

    Switch# `show vlan brief`        //查看所有VLAN的摘要信息

    Switch# `show vlan id vlan-id`        //查看指定VLAN的信息

7. 开启并查看trunk端
   
    Switch(config)#interface f0/24

    Switch(config-if)#`switch mode trunk` //将f0/24端口设置为trunk

    Switch(config-if)#`switch trunk encapsolution dot1q`//设置封装

    Switch#`show interfacef0/24   switchport` //查看f0/24的接口状态

8. 从Trunk中添加、删除Vlan
   
    Switch (config-if )# `switchport trunk allowed vlan` remove 3   //从trunk端口删除v lan3通过

    Switch (config-if)# `switchport trunk allowed vlan` add 3      //从trunk端口添加vlan3通过

    Switch # show `interface interface-id switchport`           //检查中继端口允许VLAN的列表

9. 单臂路由配置
    
    Router(config)# interface `f0/0.1`

    Router(config-subif)# `encapsolution dot1q 1 `//子接口封装dot1q 针对的是VLAN1

    Router(config-subif)# ip address  192.168.1.1 255.255.255.0 //设置VLAN的网关地址

    Router(config)# interface `f0/0.2`

    Router(config-subif)#` encapsolution dot1q 2`//子接口封装dot1q针对的是vlan2

    Router(config-subif)# ip address192.168.2.1 255.255.255.0//设置vlan2的网关的地址

10. 配置静态路由条目

    Router(config)#`ip route 192.168.10.0 255.255.255.0 192.168.9.2`
    //到达192.168.10.0网段及掩码需要经过相邻路由器的接口的IP地址

11. 配置默认路由
    
    Router(config)#`ip route 0.0.0.0 0.0.0.0 192.168.2.2`
    //所以外出的数据包如果找不到路由表目均找192.168.2.2接口

12. 配置控制台密码
    
    ```
    teacher(config)#line console 0
    teacher((config_line)#login
    teacher((config_line)#password cisco
    teacher(config)#enable password cisco//配置特权模式密码
    teacher(config)#enable secret 1234//配置加密保存的密码
    teacher(config)#service password-encryption//对所有密码加密
    ```

13. 动态路由相关命令
   
    ```
    Router(config)# router rip//启动RIP进程
    Router(config-router#version 2 //指定启动rip v2版本
    Router(config-router)# network network-number //宣告主网络号
    Router# show ip route//查看路由表
    Router#show ip route static//仅显示静态路由信息
    Router# show ip protocols //查看路由协议配置
    Rouetr# debug ip rip//打开RIP协议调试命令
    ```
14. 动态路由配置
    
    ```
    RouterA(config)#interface f0/0
    RouterA(config-if)#ip address 192.168.1.1 255.255.255.0
    RouterA(config-if)#no shutdown
    RouterA(config)#interface f0/1
    RouterA(config-if)#ip address 10.0.0.2 255.0.0.0
    RouterA(config-if)#no shutdown
    RouterA(config)#router rip
    RouterA(config-router)#network 10.0.0.0
    RouterA(config-router)#network 192.168.1.0
    ```



###### 实例

1. **实例1-基本命令**

```
Router>enable
Router#configure terminal
Router(config)#interface FastEthernet0/0
Router(config-if)#ip address 192.168.1.254 255.255.255.0
Router(config-if)#no shutdown

Router#show ip route
Codes: C - connected, S - static, I - IGRP, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
       i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
       * - candidate default, U - per-user static route, o - ODR
       P - periodic downloaded static route

Gateway of last resort is not set

C    192.168.1.0/24 is directly connected, FastEthernet0/1
C    192.168.2.0/24 is directly connected, FastEthernet0/0
S    192.168.3.0/24 [1/0] via 192.168.2.2
```
**解释**：
S：static，代表静态路由。192.168.3.0/24：目标网络号。1：管理距离0：度量值，静态路由不使用度量值对路由进行选择，视静态路由表中的路由信息为直连路由，静态路由在通常情况下优先于动态路由被使用。via：经过。192.168.2.2：出站接口，意为从该接口可以到达目标网络号。

路由度量值(Metric)表示到达这条路由所指目的地的代价，也称为路由权值(Cost)。计算路由度量值时通常会考虑：跳数、链路带宽、链路延时、链路使用率、链路可信度以及链路MTU等因素。

不同的动态路由协议会选择其中的一种或几种因素来计算度量值。在常用的路由协议中，RIP使用"跳数"来计算度量值，跳数越小，其路由度量值也就越小；而OSPF使用"链路带宽"来计算度量值，链路带宽越大，其路由度量值越小。度量值通常只对动态路由协议有意义，静态路由和直连路由的度量值统一规定为0。

通过RIP和OSPF两个协议度量值计算的参考依据可以看出，路由度量值只在同一种路由协议内有比较意义，在不同的路由协议之间路由度量值没有比较意义，也不存在换算关系。

**补充** :rocket:

-**管理距离（AD）：确定路由协议的优先级用**

为什么要出现管理距离这个技术呢?

- 在自治系统内部，如RIP协议是根据路径传递的跳数来决定路径长短也就是传输距离，而像EIGRP协议是根据路径传输中的带宽和延迟来决定路径开销从而体现传输距离的。这是两种不同单位的度量值，我们没法进行比较。为了方便比较，我们定义了管理距离。这样我们就可以统一单位从而衡量不同协议的路径开销从而选出最优路径。正常情况下，管理距离越小，它的优先级就越高，也就是可信度越高。
对于两种不同的路由协议到一个目的地的路由信息，路由器首先根据管理距离决定相信哪一个协议。

- AD值越低，则它的优先级越高。 一个管理距离是一个从0--255的整数值，0是最可信赖的，而255则意味着不会有业务量通过这个路由。

- 用来表示路由器可能从多种途径获得同一路由，例如，一个路由器要获得“10.2.0.0/24”网络的路由，可以来自RIP，也可以是静态路由。不同途径获得的路由可能采取不同的路径到达目的网络，为了区分不同路由协议的可信度，用管理距离加以表示。

- 管理距离越小，说明路由的可信度越高；静态路由的管理距离为1，说明手工输入的路由优先级高于其他的路由。

  ![router04.png](https://raw.githubusercontent.com/Sunonx/Sunonx.github.io/master/images/router04.png)

2. **实例2-远程登陆管理路由器**
   
  ```
  Router(config)#line vty 0 4
  Router(config-line)#pass
  Router(config-line)#password cisco   定义远程登录密码
  Router(config-line)#login
  Router(config-line)#exit
  Router(config)#enable password cisco   定义特权模式密码
  
  然后在pc1机上远程登录
  PC>telnet 192.168.2.2
  Trying 192.168.2.2 ...Open
   ```
  > VTY(Virtual Teletype Terminal)虚拟终端，一种网络设备的连接方式常见配置的原理:
  line是进入行模式的命令，Console、AUX、VTY、TTY……都是行模式的接口，需要用line配置。    
    VTY是虚拟终端口，使用Telnet时进入的就是对方的VTY口。   
    路由器上有5个VTY口，分别0、1、2、3、4，如果想同时配置这5口，就line vty   0   4
>



