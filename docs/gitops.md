## 技术与标准 ｜ GitOps 与 OGA

### GitOps：又一次造词运动？

伴随着 DevOps 在近些年的火爆，围绕 xOps 产生了很多概念，诸如 DevSecOps，AIOps，MLOps，ChatOps 等等，当然还有今天讲述的主角 GitOps。人们在 xOps 这条造词之路上越走越远，也从“一环”（Ops）到了“二环”（DevOps，AIOps，ChatOps 等）再到了“三环”（DevSecOps，DevBizOps GitSecOps 等），“四环”在等待大家一起创造修建。

![xops](https://github.com/majinghe/DevOps/blob/main/images/gitops/xops.png)

诚然，“造词运动”产生的概念让人们目不暇接，每一个点都意味着有新东西出来，让本来就不够用的脑容量更加捉襟见肘，唯有“躺平”以应对。但是，就算“躺平”也要积极的“躺平”，学习完 GitOps 之后躺下慢慢平复 GitOps 带来的激动心情。

GitOps 这个词出现于 2017 年，是由 weaveworks 公司根据多年云计算基础设施和应用程序管理经验而提出的一个概念。可以看出 GitOps 是非常年轻的，它的出现与云计算的大力推进有关，也可以说大胆、准确点说与**云原生**有关。

### 大名鼎鼎的云原生（Cloud Native）

现如今，没听过云原生都不好意思跟别人交流，不知道云原生都没法跟别人说组织在上云。云原生概念的提出在 2013 年，经过了这几年的演进，成立了发展势头火爆的 CNCF（Cloud Native Computing Foundation）基金会，也对与云原生的定义，有了一个大家都接受的定义：

云原生技术使企业能够在现代动态环境中构建和运行可扩展的应用程序，如公有云、私有云和混合云。**容器、服务网格、微服务、不可变的基础设施和声明式 API** 是云原生的典型技术。

> Cloud native technologies empower organizations to build and run scalable applications in modern, dynamic environments such as public, private, and hybrid clouds. Containers, service meshes, microservices, immutable infrastructure, and declarative APIs exemplify this approach.

关于云原生的更多内容，在这儿不多赘述，大家可以查看 [CNCF 官网](https://www.cncf.io)。云原生应用程序的部署是我们重点讨论的，因为它与 GitOps 密切相关。

### 云原生系统（基础设施和应用程序）管理之痛

一般情况下可以使用下面的持续交付系统（示意图）来完成云原生应用程序的部署与交付

![gitlab-gitops-push](https://github.com/majinghe/DevOps/blob/main/images/gitops/gitlab-gitops-push.png)

上述模式属于“push”模式，我称之为“一杆子到底梭哈型”（流程从左到右走到底），这是一种很常用的模式，很容易实现一键式部署。但是也存在一些问题：

* 配置仓库里清单文件（包括应用和基础设施）描述的内容是否和 Kubernetes 集群侧的实际情况是否一致
* 镜像有更新时不能够自动同步至集群侧（除非每次从头到位走一遍部署流程）
* 安全合规问题（有可能需要操作人员通过 kubectl 命令做一些集群操作）

简而言之，就是没法保证仓库清单（包括配置仓库和镜像仓库）和集群侧的实际情况相一致，集群侧的实际情况没法准确地在集群侧体现出来。长此以往，很容易发生“配置漂移”（所想不等于所得，且见下文）及安全合规问题。

> 看到了吧，编码、构建、镜像打包等都在极狐 GitLab 上完成，所谓 All in JiHu GitLab and One stop-shop DevOps platform 是也。

然而，“山重水复疑无路，柳暗花明又一村”。云原生的其中一个自带属性：**声明式** 是解决这个问题的关键点，关于声明式的理解以及解题思路可以查看如下示意图：

![gitops-mech](https://github.com/majinghe/DevOps/blob/main/images/gitops/gitops-mech.png)

声明式系统有个特点：能够帮我们自动完成应用程序（或基础设施系统）的描述状态和实际状态的自动同步，保证两者能保持一致。比如，应用部署清单里面应用程序是一个副本（replicas=1），那么集群侧应用程序就会是一个 pod。借助于这个特点，上述“push”模型的问题可以做如下解答：

既然声明式系统可以用文件清单来描述（典型如 yaml 文件），那么既然是文件就可以存储到极狐 GitLab 上（发挥了版本控制系统的功能）。开发人员或者运维人员想修改某些内容（应用程序属性、基础设施配置）的时候，只需要修改文件清单即可（修改完毕提 PR，方便 review），此时这个变更就会被自动同步至集群侧。所以现在只需要找一个方法能够自动实现这种变更监听和变更自动同步即可，而这正式今天的主角 GitOps 要做的事情。

### 呼之欲出的 GitOps

前面铺垫了这么多，GitOps 终于出现了，关于 GitOps 有这么几个特性：

* 以声明式系统（包括基础设施和应用程序）为基座（典型如 kubernetes）
* 以 Git（典型如极狐 GitLab）为单一可信源
* 一切皆代码（应用程序 & 基础设施）

使用 GitOps，上述的“push”模型就变为了下面的“pull”模型：

![gitlab-gitops-pull](https://github.com/majinghe/DevOps/blob/main/images/gitops/gitlab-gitops-pull.png)

### GitOps 之三叉戟

GitOps 的实践需要基础设施即代码（Infrastructure as Code，简称 IaC）、Pull Request（PRs）、CI/CD 三叉戟的组合拳。

#### 基础设施即代码（IaC）

基础设施即代码是一种基于使用软件开发实践来进行基础设施自动化管理的方法。它强调通过一致的、可重复的程序来对基础设施系统进行修改。当需要对基础设施进行修改时，只需要修改于基础设施相关的代码即可，随后会有自动化来测试这些变更并最终将这些变更应用到基础设施系统中。

GitOps 的重要特性之一就是：**一切皆代码**。以 Git 为单一可信源，所有与软件开发相关流程中的代码（包括基础设施代码、应用程序源码、配置等）都会存储在 Git 仓库中。

极狐 GitLab 很好的与基础设施即代码中的瑞士军刀——Terraform 做了集成，可以方便的完成云基础设施的自动化管理。详细内容和演示示例，可以查看公众号[如何借助极狐GitLab 和Terraform以代码形式构建基础设施？](https://mp.weixin.qq.com/s?__biz=Mzg5OTU3NTgyOA==&mid=2247486125&idx=2&sn=f249d96a08ba32f34f4663b3b1d9407b&chksm=c05073d6f727fac06e65349d80e73b2370c70f157cd81d19fd4f98374d1d5010dd7fa5e9fc09&mpshare=1&scene=1&srcid=0716BqeAIbnTUagNw97gp2my&sharer_sharetime=1626400478390&sharer_shareid=69a671b032908bc53da173d06860fd16&exportkey=AYaaLtwEtx9utJDAYuhe5D4%3D&pass_ticket=%2FzxWDvZPZDMJeMGsfqc4XNbLSShfgZr5OQ0iVACuyoOW4k46rKmz535cknw9gWrM&wx_header=0#rd)。

#### Pull Request（PRs）

当开发或者运维想要对系统（基础设施或者应用程序）做出某些变更时，需要提一个 Pull Request，这是一种让多人、多团队进行协作的方式，能更好的对变更进行评审（Review），提前评估变更的必要性、准确性、安全性等，从而降低变更给系统带来的风险。对系统所有的变更发起点都是代码变更，这样就使安全审计变得简单，因为一切皆代码，所见即所得，评审、审批都在仓库系统中，对于所有人员都是透明可见的，透明度也会增强团队成员之间的信任度和协作性。

#### CI/CD

当 PR 创建审核完毕，后续的变更需要 CI/CD 自动化的流程去完成系统的变更。自动化的流程减少了人为的手动干预，减少了人员误操作所带来的风险，同时能够节省时间，在大规模使用场景中，是非常重要的一环。



### GitOps 之爽

GitOps 让所有变更的发起和应用都聚焦在 GitLab 仓库中，开启了云原生时代基础设施管理和应用程序持续交付的新篇章，它能够带来以下好处：

* 快速进行变更更新和回滚

变更的更新和回滚都是通过 GitLab 的 Pull Request 来进行，可能是一个命令就能完成，简单高效。

* 人员工作体验的提升

所有人员可以通过 GitLab 进行有效的协作，那些邮件、ticket 满天飞的日子也将不复存在。GitLab 是大家都熟悉的平台，再也不用在不同工具、平台间来回切换来完成系统的变更，大家的学习成本减少了，能更好的关注在业务本身。毕竟**安安静静写代码、高技术是每个人梦寐以求的。** 

对于新入职的员工来讲，通过阅读 GitLab 仓库代码，可以快速熟悉业务、环境等内容，并用相应代码快速搭建起开发环境，从而快速融入团队，贡献自己的力量。人员培养成本降低了，工作体验提升了，对于公司来讲，做到了“降本增效”。GitOps 充分体现了**以人文本**的理念。


* 安全性提高

一切操作都是在 GitLab 的仓库上，不用再给不同人员赋予不同系统的不同权限，保证了系统的安全性，同时可以在极狐 GitLab 上通过仓库的鉴权和授权模式严格控制不同人员的不同操作权限。同时，一切变更都是自动化进行，手动操作的减少，会大大降低误操作带来的风险。

* 合规审计容易做

一切操作（哪个人员在何时做了什么操作）都在 GitLab 上一目了然（通过 PR，comment 等）。所谓所见即所得，也让合规审计变得高效、容易。

### GitOps 之殇

GitOps 用着爽，但是依旧面临一些挑战，诸如

* 协作文化的建立

GitLab 提供了一个用户体验良好的协作平台，但是使用平台的是人，协作是人与人之间、人与平台之间的协作，良好的协作需要每个人都去遵守协作流程和纪律，（诸如任何变更都应该提 PR 然后 Review 最后自动化 Apply 流程，不要手动操作，哪怕几秒能完成的小变更）。从而建立起良好的协作文化。随着公司规模的扩大，异地跨区域的协作变得越来越多，这一块儿是一个挑战，需要每一个人都参与进去，遵守流程和纪律，逐步培养出良好的协作文化。

* 敏感信息的处理

一切皆代码，意味着用户名、密码、证书、token 等敏感信息也要存储到 GitLab 仓库中，而这是兵家之大忌。不幸中之大幸就是：极狐 GitLab 和 Vault 有着完美的结合，能够很好的解决这个问题。关于这块儿后续我们会有专门的文章分析并实践。敬请期待。 

* Git workfolow 的建立

一切变更的发起、执行都在 GitLab 上，也就意味着需要建立行之有效的 Git workflow，而这在现如今多云、混合云等基础设施，采用为服务的应用程序来说是个很大的挑战。而这需要大量的测试、运行来逐步建立并完善。
