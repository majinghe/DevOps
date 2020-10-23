# 第一部分：DevOps概述

## 诞生

![](https://github.com/lhb008/DevOps/blob/main/images/timeline.png)

### 2007 年

比利时IT工程师Patrick Debois在给政府的一个数据中心做迁移的过程中，深刻的感受到了存在于开发人员和运维人员之间的一道壁垒：开发人员关心的是自己的代码，想要将代码快速推送到代码仓库，进而快速部署到生产环境上；而运维人员关心系统的稳定性，从而不能频繁、快速的将业务变更部署到生产环境上。速度与稳定就会导致矛盾的产生，由此，他就在想有没有一种方式来解决这种矛盾，打破横亘在开发和运维之间的这种壁垒呢


### 2008 年

这一年，O'Reilly出版公司在美国加州旧金山举行了第一届Velocity技术大会，旨在对Web应用程序的性能和运维展开讨论，在此次大会上有几个系统管理员和开发人员共同创建了一个 The Agile Admin的博客，目的在于分享自己的经验， The Agile Admin 的博客后来专门写了文章对于DevOps进行了详尽的阐述。当然这是后话。同年，在2008年8月的敏捷大会上，上文提到的IT工程师Patrick Debois，进行了一个主题为“如何在运维工作中应用 Scrum 和其它敏捷实践”的演讲。随后他与另外一位参会人员Andrew关于如何跨越Dev和Ops的鸿沟进行了一番长谈，为了吸引更多的人进行探讨，他们特意在Google Group 上建立了一个 Agile System Admin stration的讨论组。但是参与讨论者比较少。

### 2009年

在2009年举办的第二届Velocity技术大会上，一个主题为 10+ Deploys Per Day :Dev and Ops Cooperation at Flickr 演讲，彻底震惊了在场所有人。这次大会可以认为是DevOps雏形正式形成。这场演讲让Patrick Debois很兴奋，他似乎找到了一种方法来解开2007年以来一直困扰他的问题(打破存在与开发与运维之间的壁垒，让两者更好的进行协作)。于是在2009年他通过Twitter发出召集令，想举办一个类似Velocity的大会来探讨开发和运维的问题，结合大会主题，开发和运维，而且会议持续两天，所以他将会议名称定位DevOpsDays，有趣的是，由于Twitter有字符数限制，所以最后大会改成了DevOps大会。这宣告着DevOps的正式出现。

## 概念

维基百科对于DevOps的定义是这样的：**DevOps是让开发人员和运维人员通过协作来缩短软件开发周期，并且以持续交付方式来交付高质量软件产品的一系列实践**。在 The Agile Admin 的博客上，对于DevOps的定义：**DevOps是一种具体的实践，它需开发人员和运维人员在整个服务的生命周期内，从最开始的设计到后面的开发进程直到最后的生产运维都共同参与，通力协作**。可以简单理解为：**DevOps是IT行业的一场运动**。DevOps的目的为了**打破存在于开发人员和运维人员之间的壁垒，让开发和运维人员能够更好的合作来提高产品的交付速度**。

![](https://github.com/lhb008/DevOps/blob/main/images/devsecops.png)

## 模型

DevOps CALMS 包含五部分: Culture, Automation, Lean, Measurement, Sharing。

![](https://github.com/lhb008/DevOps/blob/main/images/calms.png)

### 文化(Culture)
其实DevOps也是一种文化: 良好的沟通与协作、无问责文化。这种文化小至团队文化，大到组织或者企业文化。

DevOps虽然是Dev和Ops的缩写，但是不仅仅是这两拨人的合作交流，而是对整个软件产品作出贡献的人都应该包含在内，这些人员的关注点不一样: 开发关注代码变更，运维关注系统稳定，测试关心测试结果，项目经理关系项目进度。因此各部分之间的沟通和协调就成了能否实现快速交付具有价值的产品这一共同目标而不可缺少的一环。

另外一个就是无问责文化，当产品出现问题的时候，第一时间大家应该做的是及时沟通，通力协作，迅速作出应对策略，而非相互指责，推诿。

除此之外，还有共享文化，创新文化等等。文化的涵盖面很广，而且文化的形成也是一个长期的过程，良好的文化是基础。如果形不成一种文化，那么所有的尝试都是没有意义的。

### 自动化(Automation)

自动化一直伴随着IT行业的发展，它的好处毋庸置疑：尽可能少的进行人为干预，就能防止由于人为误操作引起的系统崩溃，从而使得系统的有效性和鲁棒性大大增强；将产品发布流程自动化，能够提高产品的发布频率，缩短产品的发布周期；还有很重要的一点就是自动化能够节约成本。

从目前来看，自动化在DevOps中是指：将代码从变更到上生产整个流程进行自动化，也即是我们通常讲的CI/CD。因此以前有人认为DevOps就约等于CI/CD。CI/CD的概念我们后面会介绍。


### 精益(Lean)

精益产生于丰田汽车生产系统，其目的在于尽可能多的消除生产过程所产生的浪费，进而尽可能多的增加价值。将精益思想应用与IT行业，可以帮助消除软件工程和IT运维中的一些“浪费”，比如繁琐的过程，手动的流程等。在DevOps中，可以通过工具集和改进工作流程来消除上述的“浪费”，从而达到精益软件开发的目的。

### 度量(Measurement)

DevOps一定是要能够度量的，比如部署的频率，故障的修复速度，新功能的上线时间等等。没有度量，没有参考，就没法进步。度量可以是多维度的，比如可以从性能，流程，人员等一些指标来经常度量DevOps。

### 分享(Sharing)

分享是为了将一些最佳实践或者成功案例进行复制，来减少自己的工作量。如果只是蒙头闭门造车，而忘记分享，甚至不愿意分享，那么很容易形成“孤岛”思维。一旦形成“孤岛”，将会耗费大量的时间和精力来进行矫正。何况现在处于一个拥抱开源，尽情分享的时代，分享就显得尤为重要。分享可以选择不同的范围去分享，比如最佳实践和模式在团队内分享；最佳实践和模式跨团队分享；最佳实践和模式跨组织分享；最佳实践和模式在组织外部分享。范围越大说明DevOps成熟度越高。

## CI/CD

* 持续集成(Continuous Integration， CI)
持续集成是指开发人员将变更代码频繁的向主干分支集成的过程，其目的在于将代码变更可能造成的系统破坏性降到最小，一旦有问题，也能够快速的识别和隔离变更集。保证主干分支实时可用。

![](https://github.com/lhb008/DevOps/blob/main/images/devops-ci.jpg)

* 持续交付(Continuous Delivery，CD)
是一组通用的软件工程原则，允许通过使用自动化测试和持续集成频繁的发布软件新版本。持续交付可以认为是持续集成的进一步延伸。
![](https://github.com/lhb008/DevOps/blob/main/images/devops-cd.jpg)
* 持续部署(Continuous Deployment，CD)
持续部署又可以认为是持续交付的进一步延伸，指通过定义测试和验证来将风险最小化，从而将变更自动部署到生产环境中。
![](https://github.com/lhb008/DevOps/blob/main/images/devops-cde.jpg)

## 持续交付和持续部署的区别

持续交付和持续部署看起来都是将变更及时部署到生产环境中，但是他们是有差别的，持续交付通常被认为是持续集成的更进一步，它意味着可以将变更进行部署，而且部署的流程是自动化的，只要点击一个按钮，就能将变更部署到生产环境上。持续部署又是持续交付的更进一步，它意味着变更的部署没有任何的人为干预，全自动部署。另外，Jez Humble在 《持续交付》一书中提到，持续交付可以适用于任何软件开发项目，包括物联网和嵌入式项目，但是持续部署则特定于Web软件。


## Blue/Green deployment(蓝绿部署)

![](https://github.com/lhb008/DevOps/blob/main/images/blue-green.jpg)

> 蓝绿部署和 A/B Testing的区别在于，蓝绿部署的目的是为了能够使产品新版本的发布可控、稳定；而A/B测试则侧重于对于产品的功能测试。


## Canary deployment（灰度发布）
![](https://github.com/lhb008/DevOps/blob/main/images/canary.jpg)


# 第二部分： Docker 和 Kubernetes

## Docker

### 概念

一种虚拟化技术，将应用程序运行时环境进行打包封装，以达到 **build once, running anywhere**。

### 架构

![](https://github.com/lhb008/DevOps/blob/main/images/docker-arch.png)

### 核心概念

* 镜像仓库
* Dockerfile
* 镜像
* 容器

### Dockerfile 镜像 容器 关系

![](https://github.com/lhb008/DevOps/blob/main/images/dockerfile.png)


### docker 基本使用

![](https://github.com/lhb008/DevOps/blob/main/images/docker1.png)

## Kubernetes 演进史

![](https://github.com/lhb008/DevOps/blob/main/images/k8s_history.png)

Kubernetes简称K8S(除去开头的K和结尾的S，中间正好有八个字符，故号称K8S)是谷歌开源的一个全新的基于容器技术的分布式架构方案，同时也是一个全新的容器编排工具。Kubernetes的前身是谷歌的Borg系统，始于2003年，它是在谷歌内部使用的一个容器管理系统，它管理着来自数千个不同应用程序的数十万个作业，跨越许多集群，而每个集群拥有多达数万台计算机。2013年，另外一个Omega系统在谷歌内部应用，Omega可以看作是Borg的延伸，在大规模集群管理以及性能方面优于Borg。但是Borg和Omega都是谷歌内部使用的系统，也就是所谓的闭源系统。直到2014年，谷歌以开源的形式推出了Kubernetes系统，同年6月7号在github上完成了第一次提交，随后的7月10号，微软，IBM，Redhat，Docker加入了Kubernetes社区。在2015年7月Kubernetes正式发布了v1.0版本，直到今年6月19号发布了v1.15版本，而且1.16版本正在紧张开发之中。可以看出短短四年已经发布了十六个版本，而且速度越来越快。其实在容器编排领域除了有Kubernetes，还有Docker Swarm和Mesos，在初期，这三者呈三足鼎立之势，但是现在Kubernetes却一枝独秀，Kubernetes已经发展成为一个Kubernetes生态圈，而且以Kubernetes为核心发展起来的的CloudNative的发展势头也很迅猛。


# 第三部分： 基于Kubernetes的DevOps 工具链

![](https://github.com/lhb008/DevOps/blob/main/images/tool.png)
