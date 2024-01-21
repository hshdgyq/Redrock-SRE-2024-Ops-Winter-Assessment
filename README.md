2024 年红岩网校工作站运维安全部运维方向寒假考核

# 运维基础部分

由于大家现在学的东西有限，所以这部分就考察下大家的网络知识。

作为基本功，网络是必须要沉淀的一环。

lingkep刚刚学习网络，光看理论太枯燥了，一层一层的概念让他无从下手，且不知道在实际的应用，于是他决定练练手。

他已经搭建了一个局域网自己使用，网段为`172.18.100.1/24`，网关机ip为`172.18.100.1`。

①他配置好的设备可以接入校园网，他想直接在他的软路由openwrt上接入，只需配置vlan ID就可以dhcp到校园网ip，为了访问其他网段，需要写好路由，有web界面但他不想用。请你帮他写好以上配置，接口名你自己定义。 （网段分别为`10.18.0.0/12`，`202.202.32.0/20`，`219.153.62.64/26`，`222.177.140.0/25`）

②他想在服务器上创建十台Debian虚拟机(192.168.5.2-11)给朋友用，要求网关已有网关机是同一个，并且这十台虚拟机要能上网，同时网络环境要和原来网络环境隔离，分别需在网关机上做什么配置？同时，他想把某些配置命令持久化，请你帮他编写网络配置脚本与开机自启脚本。

# 开发部分

以下题目任选其一完成。

如有问题请联系出题人。

更多信息请拉到底看说明。

## **1.容器编排管理工具**

出题人：@杨鑫 

随着容器技术（如Docker）的快速发展，容器化应用程序得到了广泛的应用和接受，然而，随着应用程序数量的增加和规模的扩大，手动管理和编排容器变得非常复杂和困难。因此，Ferdinand需要一个自动化的容器编排工具来简化和优化容器集群的部署和管理流程。

### **level0**

**容器生命周期管理**: 

你需要编写脚本来管理容器的生命周期，可以使用Docker SDK（Docker Engine API的Python库）来与Docker引擎进行交互，脚本可以提供命令或函数，基本的功能必须要实现，比如创建容器、启动容器、停止容器、重启容器和销毁容器等操作，来管理容器的运行状态。

### **level1**

**服务发现**: 

要知道，在一个完整的服务中可包括多个容器实例，你需要在整个服务跑起来的同时内部容器能够彼此发现调用，可参考docker-compose，使用python脚本来编排，实际上程序最终还是会转化做 docker-compose 脚本执行。但是这种写法的优点是更灵活，你可以在程序中使用 if, while, 链接数据库，等等操作，可以做更复杂的容器编排。因此，编写脚本来编排容器使其能够跑一个完整的服务

### **level2**

**负载均衡**: 

负载均衡是一个基本的网络服务，主要是为了解决并发压力，增强网络处理能力减轻单个设备的资源压力，提高整体服务性能，对于负载均衡的实现，可以使用Docker+Nginx代理服务，你可以通过编写脚本来自动配置负载均衡规则，从而平衡请求流量，并将其分发到集群中的多个容器实例。

### **level3**

**自动伸缩**:

我们对于流量进行了外部处理，那内部同样也可以应对流量的变化而变化，你需要设计脚本来监控容器集群的负载情况，并根据设置的策略自动进行伸缩，通过监控集群中容器实例的指标，比如CPU使用率或请求处理时间，脚本可以自动扩展或缩减容器实例的数量，从而能够应对流量的动态变化。

### **level4**

**健康检查和故障恢复:**

由于我们不能时刻盯着容器的运行状态，所以我想你能够编写脚本对容器进行健康检查和故障恢复，你可以使用Docker的健康检查功能来监测容器实例的健康状态。通过配置健康检查命令或脚本，并结合Docker的自动容器恢复功能，可以实现容器的自动故障恢复。当健康检查失败时，脚本可以自动重启或迁移不健康的容器实例。

### **ps:**

想做一个完整的系统可以使用多个脚本来实现不同的功能模块，然后通过编排这些脚本来构建一个完整的容器编排和管理系统。每个脚本可以负责一个特定的任务，通过将这些脚本组织在一起，并使用适当的调度和协调机制（如使用Python的subprocess、threading模块或其他类似的工具），可以实现一个相对完整的容器编排和管理系统。

(**最低完成level2**)

## 2.**iManager-您的私人镜像管家**

出题人：@李逸雄 

尽管Docker官方提供了公共的镜像仓库DockerHub，但从安全性和稳定性等方面考虑，部署私有镜像仓库是非常有必要的。Harbor是一个由VMware公司开源的企业级的Docker Registry管理项目，是我们搭建私有镜像仓库的不二之选。

而自动化一直是运维工作中的重中之重。

Yiiong希望你能够将Harbor与飞书机器人联系起来，方便管理员统一管理镜像，使管理员随时都可以知晓仓库镜像的变动信息，管理员动动手指就可以对仓库里的镜像进行操作等。

### **前置准备**

- 建议使用服务器搭建Harbor仓库，并且配置好https
- 申请一个飞书企业账号
- 可能需要一个域名？

### **任务**

完成至Level X（X≥1）+Level 4哦！

#### **友善的用户交互**

用户肯定需要知道你的机器人都可以干些什么事情吧！

用户向机器人发送`帮助`，机器人返回可以实现的功能列表。

当用户发送了一些乱七八糟的信息时，机器人需要做出一定的回复，比如`我听不懂捏`。

#### **Level 0 通知**

当镜像状态发生改变时，机器人向管理员发起通知。

通知内容包括：

1. 镜像状态（Push or Pull or Delete）
2. 镜像名称以及标签
3. 镜像状态改变的日期
4. 镜像状态改变者

#### **Level 1 简单查询**

管理员向机器人发送`查询项目`，机器人返回所有项目的名称、所属者以及访问级别。

管理员向机器人发送`查询仓库`，机器人返回所有仓库的名称、创建时间以及更新时间。

#### **Level 2 镜像管理**

在我们的团队开发过程中，难免会出现多次推送镜像但镜像测试不通过的情况。

Yiiong希望当镜像被以Push状态推送时，通知内容中新增加一个超链接按钮，点击这个按钮即可删除这个镜像。

另一种方式是，向机器人发送`删除镜像：镜像名`，即可删除某个镜像

#### **Level 3 用户管理**

我们的整个仓库不可能只有一个管理员用户，管理员经常需要为不同的成员创建不同的用户。

Yiiong希望管理员向机器人发送`创建用户：用户名-密码-邮箱`即可创建一个新用户，

并且可以将特定用户以开发者身份加入到特定项目的成员中。

#### **Level 4 打包**

编写Dockerfile，将你的所有文件用Docker打包制作成镜像，使其他用户填入一些必要的信息就可以愉快地使用你的作品辣！   

### **加分项**

1. 发挥你的奇思妙想，实现一些意想不到的功能。
2. 使用Kubernetes完成必要的内网穿透。
3. 使用UptimeKuma监控你的仓库，当出现问题时通过机器人返回一些必要信息。
4. 飞书开放平台提供了一种美观的”卡片式“消息，使用它的话答辩的时候一定很潇洒啊！

## 3.lingkep的造轮子计划

出题人：@刘泉 

随着当下年轻人开发的欲望愈加强烈，为了深入了解操作系统，提升开发能力，lingkep想让你帮他写点东西。

题目内容:

参考POSIX API，写个壳

#### level0

最基本的要求，把你写完的程序打包成镜像，可以一键运行。

#### level1

实现像mkdir，cd，exit这样的基础命令，可以自己想，实现5个即可。

#### level2

可以执行某些程序(不能跑程序怎么叫壳呢)。

#### level3

实现输入/输出重定向，更多的，还可以实现 2>、>>、&>、2>>、pipe......

#### level4

结合你学过的网络知识，实现ping,traceroute等命令。

#### levelN

自己发挥。实现你认为有趣的功能。

### 注意事项

你需要先了解shell的工作流程。实现的功能应该规范化，比如输入的命令发生传参错误的处理，比如cd命令不传参默认进入的目录，比如子进程的运用等等。

最低完成level2+level3的输入输出重定向。

# 说明
- 截止时间:<br/>
    运维部分: 2024 年 2 月 1 日 23:59 <br/>
    开发部分: 2024 年 2 月 21 日 23:59
- 提交方式：Fork 此项目，在对应题目的文件夹下放入你的工程文件夹，工程文件夹以你的学号命名，运维部分交到ops，然后提出 Pull Request。
- 语言不限，鼓励大家在寒假自学语言。推荐大家使用Python完成考核。
- 提交开发部分的时候应该带有一个`README.md`，详细地说明你的程序能够做哪些工作，有哪些功能还没有实现，有哪些 bug等。
- 尽量完成每道题的基础要求吧。截止的时候即使没做出来，也要尽量交，做到多少算多少。
- 不要照抄代码，至少你得把变量名给我改一下吧？我说的是，提交的内容不要照抄网上的，也不要大片大片原封不动地抄GPT。**我们希望GPT是你的老师而不是你的仆人**你可以参考GPT，学的时候，理清思路了自己再重写一遍，就是学习了~
- 尽最大努力去做，实在不会的知识线上来问我们，我们都比较乐意。
- **不要抄代码！！！不要抄代码！！！不要抄代码！！！后果自负**。
