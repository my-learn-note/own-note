# EC2

## EC2的类型

![image-20230307191342325](https://picgo-starry.oss-cn-beijing.aliyuncs.com/img/devops/AWS/ec2-type.png)

## 计费方式

![image-20230307192249297](https://picgo-starry.oss-cn-beijing.aliyuncs.com/img/devops/AWS/charge-type.png)

竞价类型有可能会被强行停止。如果同region别人用了闲置的计算资源

## EC2的存储类型

### 实例存储

#### **什么是实例存储**

实例存储为您的实例提供临时性块级存储。此存储位于己物理附加到主机的磁盘上。实例存储是一种理想的临时存储解决方案，非常适合

存储需要经常更新的信息，如缓存、临时数据和其他临时内容，或者存储从一组实例上复制的数据，如 Web服务器的负载均衡池。

#### 特点

- 实例存储为 EC2 实例提供了短暂的块存储设备

   实例存储 (Instance Store Volumes）又叫做短暂型存储 (Ephemeral Storage)

- ﻿实例存储是 AWS 的宿主机上依附的存储（可以理解为实例存储是真实的物理机上安装的磁盘）

   实例存储比较适合存放短哲型、变化很快的数据，比方说缓存、爬虫数据和其他短哲的数据

- ﻿实例存储的大小取决于实例的类型

- ﻿实例存储的存活与否与实例的状态有关系

  - 实例重启，实例存储的数据将不受影响
  - 一旦实例终止、休眠或者停止，实例存储将永久消失
  - 实例存储的实例不能进入停止状态（Stop），只能重启（Reboot）或者终止（Terminate）

### EBS存储

#### 什么是EBS存储

Amazon Elastic Block Store (Amazon EBS) 提供了块级存储卷以用于 EC2 实例。EBS 卷的行为类似于原始、未格式化的块储存设备。您

可以将这些卷作为设备挂载在实例上。附加到 EBS 实例的卷公开为独立于实例生命周期而持续存在的存储卷。您可以在这些卷上创建文

件系统，或者以使用块储存设备(如硬盘）的任何方式使用这些卷。您可以动态更改附加到实例的卷的配置。

#### 特点

- 亚马逊 EBS 卷提供了高可用、可靠、持续性的块存储，EBS 可以依附到一个正在运行的EC2 实例上

- ﻿如果你的 EC2 实例需要使用数据库或者文件系统，那么建议使用 EBS 作为首选的存储设备

- ﻿EBS 卷的存活可以脱离 EC2 实例的存活状态。也就是说在终止一个实例的时候，你可以选择保留该实例所绑定的 EBS 卷

- ﻿EBS 卷可以依附到同一个可用区（Az）内的任何实例上

-  EBS 卷可以被加密，如果进行了加密那么它存有的所有已有数据，传输的数据，以及制造的镜像都会被加密

- ﻿EBS 卷可以通过快照 (Snapshot）来进行（增量）备份，这个快照会保存在 S3 (Simple Storage System)上

- ﻿你可以使用任何快照来创建一个基于该快照的 EBS 卷，并且随时将这个 EBS 卷应用到该区域的任何实例上

-  EBS 卷创建的时候已经固定了可用区，并且只能给该可用区的实例使用。如果需要在其他可用区使用该 EBS,那么可以创建快照，并

  且使用该快照创建一个在其他可用区的新的 EBS 卷

- 快照可以被复制到其他可用区

#### EBS的不同类型

SSD: Solid State Disk(固态硬盘)

HDD: Hard Disk Drive(机械硬盘)

Amazon EBS 提供以下卷类型：通用型 SSD （gp2 和 gp3）、预置 IOPS SSD (io1 和io2）、吞吐量优化型 HIDD (stI)、ColdHDD (SC1)以

及磁介质卷(standard)。它们的性能特点和价格不同，您可根据应用程序要求定制您所需的存储性能和相应费用。

![image-20230308001221776](https://picgo-starry.oss-cn-beijing.aliyuncs.com/img/devops/AWS/ebs-type.png)



![image-20230308001429252](https://picgo-starry.oss-cn-beijing.aliyuncs.com/img/devops/AWS/ebs-type2.png)

### 对比

| EC2实例存储            | EBS存储                  |
| ---------------------- | ------------------------ |
| 实例的宿主机的本地存储 | 虚拟化的存储             |
| 适合临时性的存储       | 适合长久的数据存储       |
| 数据没有高可用         | 数据在可用区内有多份备份 |
| 不能做快照             | 可以做快照               |
| 提供SSD和HDD           | 提供SSD和HDD             |



## AMI系统镜像和快照

### 什么是AMI

Amazon Machine Image(AMI)提供启动实例所需的信息。在启动实例时，必须指定AMI。在需要具有相同配置的多个实例时，可以从单

个AMI启动多个实例。在需要不同的配置的实例时，可以使用其他AMI启动实例

![image-20230308003703150](https://picgo-starry.oss-cn-beijing.aliyuncs.com/img/devops/AWS/AMI-process.png)

Amazon Linux 2 和 Amazon Linux AMI 是 AWS 提供、支持和维护的 Linux 镜像。以下是一些主要功能：

- ﻿对于 Amazon EC2 用户没有额外费用

- 稳定、安全和高性能的执行环境，适用于 Amazon EC2 上运行的应用程序

- ﻿对多个版本的 MySOL、 PostgresQL、Python、Ruby、Tomcat 及许多常见软件包的存储库访问权限

- ﻿定期更新以包括最新组件，这些更新也可在 yum 存储库中使用，适用于安装在运行中的实例上

-  包括可与 AWS 服务轻松集成的软件包，如AWS CLI Amazon EC2 API 和 AMI 工具、适用于

   Python 的Boto 库以及 Elastic Load Balancing 工具

- 创建镜像的时候，也会创建一个EBS快照

### 快照

可以通过拍摄时间点快照将 Amazon EBS 卷上的数据备份到 Amazon S3。 快照属于增量备份，这意味着仅保存设备上在最新快照之后更

改的数据块。由于无需复制数据，这将最大限度缩短创建快照所需的时间和节省存储成本。每个快照都包含將数据（拍摄快照时存在的数

据）还原到新 EBS 卷所需的所有信息。

![image-20230308004511775](https://picgo-starry.oss-cn-beijing.aliyuncs.com/img/devops/AWS/snapshot-time.png)

快照只会存储硬盘中的内容，不会存储内存中的内容，如果EC2实例是运行状态，建议先stop(如果内存中还有数据，会把内存的数据写入

到硬盘)，否则可能会丢一些数据



#### 特点

- 备份的快照将会保存在**亚马逊S3 (Simple Storage System)**上, 但是不能被访问，是不可见的
- EBS快照属于**增量备份**，即第二次之后的快照只会更新变化了的那一部分数据
- 你可以在EC2实例运行的状态下进行EBS的快照操作，但会给EC2的系统带来一定延迟（CPU，内存利用率会变高）
- 最佳实践是将EC2实例停止，然后将EBS从EC2上卸载下来，进行快照操作
- 你可以基于EBS快照在**同一个AWS区域**创建新的EBS卷，这个卷可以是任何EBS类型，任何支持的大小
- 你也可以将快照复制到其他AWS区域
- 你可以将快照共享给其他的AWS用户
- 加密的EBS卷在创建快照后，该快照也会被自动加密
- 通过加密快照创建的EBS也是自动加密的
- 在复制未加密的快照时，你可以在复制过程中对其加密



#### 常用场景

如果你想将一个EC2实例从一个AWS区域迁移到另一个AWS区域，你需要：

1. 创建基于这个EC2实例的AMI

2. 将这个AMI进行复制，复制到另一个AWS区域

3. 通过这个AMI创新创建一个EC2实例

4. 充当数据盘的EBS也需要做EBS快照

5. 将这个EBS快照进行复制，复制到另一个AWS区域

6. 通过这个EBS快照创建EBS卷，并且依附到EC2实例上去

   

如果你想复制一个EBS卷到该AWS区域的不同可用区，你可以：

1. 创建一个EBS快照
2. 通过EBS快照创建一个新的EBS卷，并且定义大小、卷类型、是否加密等属性



## EC2的生命周期



![image-20230308193722695](https://picgo-starry.oss-cn-beijing.aliyuncs.com/img/devops/AWS/ec2-lifecycle.png)

### 休眠

当使实例休眠时，EC2会向操作系统发出信号来执行休眠。休眠会将实例内存中的内容保存到EBC根卷。EC2保存树立的EBS根卷和任何附

加的EBC数据卷

在启动实例时：

- EBS根卷会恢复为之前的状态
- 会重新加载RAM(内存)中的内容
- 回复实例上之前运行的进程
- 之前附加的数据卷会重新附加，实例也会保留其实例ID

![image-20230308194845211](https://picgo-starry.oss-cn-beijing.aliyuncs.com/img/devops/AWS/ec2-hibernation.png)



## 负载均衡器(Load Balance)

### **弹性负载均衡器（Elastic Load Balancing）**

充当了最终用户的单一触点，将访问ELB的流量分配到处于**多个可用区**的**多个EC2实例**之间。可以根据需要在负载均衡器中添加或删除EC2实例，但不中断应用程序的功能和业务。

### 应用负载均衡器(Application Load Balancer)

应用负载均衡器为你的HTTP或者时HTTPS流量提供了灵活的路由选项，后端可以接常见的虚拟机、微服务和容器

![image-20230309235812896](https://picgo-starry.oss-cn-beijing.aliyuncs.com/img/devops/AWS/alb.png)

**ALB**充当客户端的单一接触点。负载均衡器在多个可用区中的多个目标间分配应用程序的传入流量。这将提高应用程序的可用性。可以添

加若干个监听器

**监听器**使用配置的**协议和端口**检查来自客户端的连接请求。监听器的规则确定ALB如何将请求路由到其目标

每个目标组使用指定的协议和端口号将请求路由到一个或多个注册目标，可以对每个目标组配置运行**状况检查**

![image-20230310001110603](https://picgo-starry.oss-cn-beijing.aliyuncs.com/img/devops/AWS/ALB-listener.png)



### 网络负载均衡器(Network Load Balancer)

网络负载均衡器适用于超高性能、大批量TLS负载的应用。它支持UDP和静态IP地址

![image-20230309235837080](https://picgo-starry.oss-cn-beijing.aliyuncs.com/img/devops/AWS/nlb.png)

网络负载均衡在开放系统互连 （OSI)模型的第四层运行。它每秒可以处理数百万个请求。在负载均衡器收到连接请求后，它会从默认规则

的目标组中选择一个目标。

- ﻿﻿NLB 可以基于协议、源卫地址、源端口、目标 IP 地址、目标端口和 TCP 序列号，使用流式哈希算法选择目标
- ﻿﻿NLB 可以每秒处理数百万个请求
- ﻿支持静态IP 地址（弹性 IP）用于负载均衡器
- 同 ALB一样，NLB 支持通过 IP 地址进行目标注册，包括位于 VPC 之外的目标
- ﻿支持容器化的应用程序
- ﻿Network Load Balancer 不能关联安全组

### 网关负载均衡器(Gateway Load Balancer)

能够部署、扩展和管理虚拟设备，例如防火墙、入侵检测和防御系统及深度数据包检测系统

![image-20230309235906971](https://picgo-starry.oss-cn-beijing.aliyuncs.com/img/devops/AWS/GLB.png)



### ALB vs ELB

- Application Load Balancer可以进行基于路径的路由。即可以根据用户请求中的URL字段不同来将请求发送到不同的目标组中。比方

  可以定义ELB，将访问**/post**的流量转发到目标组1中，然后将访问**/send**页面的流量转发到目标组2中，那么就可以把原本的一个网页

  应用程序分解成更小的服务单元

- ALB可以侦听HTTP数据包头部的信息，根据此字段来定义规则

- ALB支持通过IP地址进行目标注册，包括位于VPC之外的目标。即可以在一个ALB中定义4个AWS中的EC2实例，同时定义2个来自公司

  内网的物理服务器

- 支持容器化的应用程序

### DNS 解析

ALB 会以 DNS (Domain Name System)的形式显示在 AWS 管理控制台，并且会动态解析不同公网IP地址，我们在使用 ALB时要尽量用 DNS 来对它进行访问，而不是 IP地址。

### 健康检查

每个负载均衡器节点仅将请求路由至负载均衡器的已启用可用区中的正常目标。每个负载均衡器节点均使用每个目标注册

到的目标组的运行状况检查设置来检查该目标的运行状况。在注册目标后，目标必须通过一次运行状况检查才会被视为正常。

### 粘性会话 (Sticky Sessions/Session Affinity)

默认人情况下，ALB 会根据选定负载均衡算法将每项请求单独路由到已注册的目标。但

是，可以使用粘性会话功能（也称为会话关联），使侦载均衡器能够将用户会话绑定到特定的目标。这可确保在会话期间将来自用

户的所有请求发送到同一目标中。对于维护状态信息以便向客户端提供持续体验的服务器来说，此功能很有用。要使用粘性会话，客

户端必须支持 Cookie

### 连接耗尽 (Connection Draining)

要确保 Classic Load Balancer 停止向正在取消注册或运行状况不佳的实例发送请求，并使现有连

接保持打开状态，请使用连按耗尽。这将使负载均衡器能够完成向正在取消注册或运行状况不佳的实例发出的进行中请求



















