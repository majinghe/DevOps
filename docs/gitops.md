## 技术与标准 ｜ GitOps 与 OGA

### GitOps：又一次造词运动？

伴随着 DevOps 在近些年的火爆，围绕 xOps 产生了很多概念，诸如 DevSecOps，AIOps，MLOps，ChatOps 等等，当然还有今天讲述的主角 GitOps。人们在 xOps 这条造词之路上越走越远，也从“一环”（Ops）到了“二环”（DevOps，AIOps，ChatOps 等）再到了“三环”（DevSecOps，DevBizOps GitSecOps 等），“四环”在等待大家一起创造修建。

![xops](https://github.com/majinghe/DevOps/blob/main/images/gitops/xops.png)

诚然，“造词运动”产生的概念让人们目不暇接，每一个点都意味着有新东西出来，让本来就不够用的脑容量更加捉襟见肘，唯有“躺平”以应对。但是，就算“躺平”也要积极的“躺平”，学习完 GitOps 之后躺下慢慢平复 GitOps 带来的激动心情。

GitOps 的出现与云计算的大力推进有关，准确点，大胆点说与**云原生**有关。

### 大名鼎鼎的云原生（Cloud Native）

现如今，没听过云原生都不好意思跟别人交流，不知道云原生都没法跟别人说组织在上云。云原生概念的提出在 2013 年，经过了这几年的演进，成立了发展势头火爆的 CNCF（Cloud Native Computing Foundation）基金会，也对与云原生的定义，有了一个大家都接受的定义：

云原生技术使企业能够在现代动态环境中构建和运行可扩展的应用程序，如公共云、私有云和混合云。**容器、服务网格、微服务、不可变的基础设施和声明式 API** 是云原生的典型技术。

> Cloud native technologies empower organizations to build and run scalable applications in modern, dynamic environments such as public, private, and hybrid clouds. Containers, service meshes, microservices, immutable infrastructure, and declarative APIs exemplify this approach.

关于云原生的更多内容，在这儿不多赘述，大家可以查看 [CNCF 官网](https://www.cncf.io)。云原生应用程序的部署是我们重点讨论的，因为它与 GitOps 密切相关。

### 云原生应用的持续交付

一般情况下可以使用下面的持续交付系统（示意图）来完成云原生应用程序的部署与交付

![gitlab-git-pull](https://github.com/majinghe/DevOps/blob/main/images/gitops/gitlab-git-pull.png)

上述模式属于“push”模式，我称之为“一杆子到底梭哈型”（流程从左到右走到底），这是一种很常用的模式，很容易实现一键式部署。但是也存在一些问题：

* 配置仓库里清单文件（包括应用和基础设施）描述的内容是否和 Kubernetes 集群侧的实际情况是否一致
* 镜像有更新时不能够自动同步至集群侧（除非每次从头到位走一遍部署流程）
* 安全合规问题（有可能需要操作人员通过 kubectl 命令做一些集群操作）

简而言之，就是没法保证仓库清单（包括配置仓库和镜像仓库）和集群侧的实际情况相一致，集群侧的实际情况没法准确地在集群侧体现出来。长此以往，很容易发生“配置漂移”（所想不等于所得，且见下文）及安全合规问题。

然而，“山重水复疑无路，柳暗花明又一村”。云原生的其中一个自带属性：**声明式** 是解决这个问题的关键点，关于声明式的理解可以查看如下示意图：

![gitops-mech](https://github.com/majinghe/DevOps/blob/main/images/gitops/gitops-mech.png)


