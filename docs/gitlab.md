# 极狐 GitLab 探秘系列 ｜理论篇之极狐 GitLab 初探

## 极狐 GitLab *VS* GitLab

众所周知，GitLab 是全球领先的一体化 DevOps 平台，但是发源于国外的 GitLab 在赋能国内企业发展方面还是存在诸多限制和不变，为了让众多国内用户能体验极致的 GitLab 体验，在 GitLab 与红杉宽带跨境数字产业基金以及高成资本的大力推动下，成立了极狐 GitLab。极狐 GitLab 和 GitLab 美国的协作模式大题如下：

* 极狐 GitLab 依旧基于 GitLab 主干分支开发（这也是开源产品能够保持长久竞争力的有效手段之一，不分叉）
* GitLab 源代码会实时同步至极狐在国内的服务器
* 源代码新增极狐目录，主要针对国内用户进行相关功能开发（开发更贴合中国人习惯、思维的产品）

一言以蔽之：**极狐 GitLab 和 GitLab 属于同宗同源，秉持开放核心和开源应用的宗旨，极力打造更符合中国市场的一体化 DevOps 平台**。更多关于极狐 GitLab 的信息，可以查看极狐 GitLab 公众号、视频号或者官网。
 
## 极狐 GitLab 不仅仅是代码托管平台

重要的话要说在、写在最前面，而且应该是多遍：**GitLab 不仅仅是一个代码托管平台，而且一个一体化的 DevOps 平台。它是一个平台，关于 DevOps 的，而且最最重要的是它是一体化的。**


一体化即覆盖软件开发的整个生命周期(software development life cycle，SDLC)

![sdlc](https://github.com/majinghe/DevOps/blob/main/images/gitlab-4.png)


不信？先看看 [CNCF 持续交付技术雷达](https://radar.cncf.io/2020-06-continuous-delivery)。众所周中，持续交付（Continuous Delivery）是 DevOps 实践的核心关键能力，也是各个企业或者组织积极推进 DevOps 落地所追求的目标。从技术雷达看，GitLab 赫然在列，而且在 TRIAL 阶段。足以佐证最开始的阐述：**GitLab 不仅仅是一个代码托管平台，它还是关于 DevOps 的一个平台**，至于是怎样的一个平台，看完下面的内容，相信你会有自己的判断。

![gitlab](https://github.com/majinghe/DevOps/blob/main/images/radar.png)

> 关于技术雷达的相关内容，大家可以查看 CNCF 官网。

## 极狐 GitLab 揭秘

DevOps 出现也有十多年了，最近几年呈火爆的发展趋势，我们可以先不用管 GitLab 有什么，先想想我们如果要推进 DevOps 落地的话，我们会关心哪些问题。

### 敏捷开发管理

极狐 GitLab 敏捷开发管理能够将面向功能需求（用户需求）文档转换成面向价值的用户故事（开发人员能看得懂的开发需求），完成了用户需求到开发需求的转换。整个过程都是可视化的，可以清晰的看到用户需求的详尽描述、功能开发的进度跟踪等。对于敏捷项目开发中的各个阶段、各种信息都有详尽描述、可视化的报表，能够很好的为项目开发保驾护航。

此外，极狐 GitLab 和 Jira、禅道都可以进行深入的集成融合。

### 代码托管

代码毫无疑问是我们最看重的，也是我们 IT“打工人”在经历 996/007 福报之后的智慧结晶。代码托管也是 GitLab 最基本的功能之一，分支管理（branch）、代码审查（review）、代码合并（merge）等都是一应俱全。熟悉 Git 操作的小伙伴可以很快上手 GitLab。 


### CI/CD(极狐 GitLab Runner）

CI/CD（continuous integration/continuous deployment(delivery)) 是 **DevOps 落地实践的两大核心关键能力**。甚至有很多企业或者组织认为实现了 CI/CD 就等于落地了 DevOps。可见 CI/CD 的重要性。GitLab 同样提供了出色的 CI/CD 功能，比如说只需要简单的配置一下 `.gitlab-ci.yml` 文件，就可以体验 CI/CD 功能。如下所示，就是一个输出“Hello World”的配置文件示例。（“Hello World 是程序员认知世界万物的开始）
```
job:
  script:
    - echo "Hello World, This is GitLab"
```

> 当然，CI/CD 的使用要从托管项目的实际出发，书写并调试正确的配置文件。

极狐 GitLab Runner 是极狐 GitLab 实现 CI/CD 的基石。极狐 GitLab Runner 能够让开发者针对不同分支进行相应的 CI/CD 流水线设计，而且整个构建过程的产物、结果都是可视化的，同时具有原生支持容器（Docker）、多语言支持、Runner 自动伸缩、多系统（Linux、Mac、Windows、FreeBSD）支持等特点。当然，如果用户不想用 GitLab 自身提供的 Runner，还可以自定义 Runner（将自己的服务器配置为 Runner 可运行的环境，再将 Runner 和极狐 GitLab 相连接），这样就省去了由于构建过多而需要等待的烦恼。


### 镜像仓库

随着云原生浪潮的席卷，软件的交付模式也从源码交付变成了镜像交付。镜像在云原生应用的部署与管理中占据着重要的位置。GitLab 同样有容器镜像仓库，可以像使用其他镜像仓库一样来使用 GitLab 的容器镜像仓库，比如

```
$ docker login registry.gitlab.com -u username -p password
$ docker build -t registry.gitlab.com/username/demo
$ docker push registry.gitlab.com/username/demo

```

当然，最简单的就是配置在 CI/CD 流水线里面，等镜像构建完毕，自动推送至镜像仓库，代码如下：

```
docker-build:
  # Use the official docker image.
  image:
    name: gcr.io/kaniko-project/executor:debug
    entrypoint: [""]
  script:
    - mkdir -p /kaniko/.docker
    - echo "{\"auths\":{\"$CI_REGISTRY\":{\"username\":\"$CI_REGISTRY_USER\",\"password\":\"$CI_REGISTRY_PASSWORD\"}}}" > /kaniko/.docker/config.json
    - /kaniko/executor --context $CI_PROJECT_DIR --dockerfile $CI_PROJECT_DIR/Dockerfile --destination $CI_REGISTRY_IMAGE:$CI_COMMIT_TAG
  rules:
    - if: $CI_COMMIT_BRANCH
      exists:
        - Dockerfile
```
### DevSecOps

安全永远是一个很重要的话题，以往的瀑布式开发中，安全是被滞后的（在测试甚至更靠后的阶段），留给安全的时间是相对比较充裕的；随着项目开发的敏捷化，早发布、快发布已经成为了主旋律，在这种情况下，安全需要被提前，也就是常说的安全左移（Security Shift Left），左移至编码，甚至计划阶段，并且对于安全测试也要做到自动化。

> 测试领域有一个原理：在需求阶段发现并修复一个缺陷或问题如果如需要花费一美分，那么在开发阶段修复同样的问题则需要花费十美分；在测试阶段话花费一美元，在生产环境则需要十美元。

基于此，极狐 GitLab 提供了覆盖软件开发生命周的 DevSecOps 解决方案。包含但不仅限于下述的内容：

* **敏感信息扫描**：很多时候，开发人员为了方便本地调试代码，会将数据库用户名密码、API token 等敏感信息做一些硬编码（Hard Code）。此类代码提交后，就造成了敏感信息泄漏，存在系统被黑客攻击的重大风险。极狐 GitLab 针对这种情况，会有一个敏感信息扫描机制，及时发现代码仓库中的敏感信息，并将结果进行展示、告警，通知相关人员及时快速处理。

* **镜像扫描**：如果说容器是云原生时代的一大核心，那么镜像就是容器的灵魂。保证镜像的安全，及时发现漏洞存在的镜像，会在很大程度上保证应用程序的安全。GitLab 的容器镜像仓库自带镜像扫描机制，能在第一时间对推送的镜像进行扫描并给出相应的报告。

* **安全测试**：极狐 GitLab 提供常用的安全测试，诸如 SAST(Static Application Security Testing)、DAST(Dynamic Application Security Testing) 来对源码及应用进行安全测试。通过分析代码找出已知安全漏洞，出具漏洞报告。

* **依赖分析与扫描**：通过分析依赖关系中的漏洞来对应用程序的安全性进行评估。

* **license 扫描**：企业对于开源的使用率在逐年上升（有数据显示，企业的开源采用率甚至达到 80% 以上）。开源的使用能够加速企业创新，但是使用开源必须要遵从开源合规。基于此，极狐 GitLab 会对项目中包含的相关 license 进行合规扫描，并出具 license 合规报告。

* **漏洞管理与分析**：针对扫描出来的漏洞能够输出详细的文档，诸如漏洞影响、漏洞修复等步骤，可以帮助用户快速修复漏洞并进行追踪。



## GitOps

云原生是时下非常火热的一个词语，其目的是充分利用云平台的红利，但是云原生应用的管理始终是一个复杂的问题。GitOps 提供了一种云原生应用管理的新模式：以声明式系统（如 Kubernetes）为基座，以 Git（GitLab、GitHub 等）为单一可信源来帮助开发、运维人员方便有效的管理云原生应用。为了更好的推动 GitOps 的发展，极狐 GitLab 联合中国信息通信研究院、云原生计算基金会（CNCF）共同发起了“开源 GitOps 产业联盟”（Open GitOps Industry Alliance，简称 OGA 联盟）。更多关于 OGA 的信息可以查看[新闻速递 | 极狐(GitLab)携手CNCF成立“开源GitOps产业联盟” 推动中国开源生态发展](https://mp.weixin.qq.com/s?__biz=Mzg5OTU3NTgyOA==&mid=2247485899&idx=2&sn=1a9d91c8c8089bddefbe75d7465f7cbe&chksm=c05070b0f727f9a6ffe9260c869ca24fe3782c4f86335c9c0dc2127706607948859d6dd1be54&mpshare=1&scene=1&srcid=0701wi0GJlTgvueXrX5C9E2d&sharer_sharetime=1625108476184&sharer_shareid=69a671b032908bc53da173d06860fd16&exportkey=ASJR06cSHs6%2BRPzCyS2Ei8A%3D&pass_ticket=QsMXW%2BzV0CTlwzjnv5eCAokwyYIMUDVADT4%2BqXJBW%2FGXkzcl5SJaxoxhpinrPE3E&wx_header=0#rd)


## 度量

没有度量就没有进步。度量是 DevOps 中非常重要的一环（DevOps 的 CALMS 模型中的 M 就代表度量（Measurement））。极狐 GitLab 提供了四个关键指标来对 DevOps 做出度量，分别是：

* 前置时间：开始编码到部署所耗费的时间。如果变更前置时间过长，可能意味着开发或 部署过程的某些环节出现了问题或阻碍。
* 部署频率：吐吞量的另一种度量方式，更频繁的部署往往意味着单次部署包含的变更更少，但对于某个特性来说，可以更快地获得产生价值，获得实际反馈。
* 变更失败率：发生变更后出现故障的几率。如果变更失败率居高不下，可能意味着在过程或工程实践中出现了某些问题或阻碍。
* 服务恢复时长：当服务中断或降级后，需要花费多少时间将服务恢复正常。每次部署包含的变更多寡、技术债务堆积程度对该指标有一定影响。

当然，除此以外，极狐 GitLab 还有针对系统的总户用、研发项目、流水线、合并请求等的众多内置度量分析。分析的结果均以可视化的方式呈现。

## 日志和监控

日志和监控其实是伴随软件开发的整个生命周期的，GitLab 提供的日志和监控系统能够为开发、测试、运维等人员提供关于应用程序的详细情况，方便人们随时掌握应用程序的状况。


当然，GitLab 还有其他关于安全方面的功能，详细内容可以查看[这儿](https://about.gitlab.com/direction/secure/#security-paradigm)或者[这儿](https://docs.gitlab.com/ee/user/application_security/configuration/)。也敬请期待我们后续文档对此类内容详细的讲解。


## 一体化 DevOps 平台的好处

### 提升开发体验

这一点就像大家去万达一样，购物、娱乐、餐饮应有尽有，消费者不用出万达商城就能满足一切需求，省去了大家在不同地点来回折腾的烦恼。GitLab 的一体化DevOps 平台提供了用户的所有需求，用户只需要在这一个平台就能完成所有操作，不用在构建时切到构建工具的地址，镜像扫描切到镜像系统（上云的用户一般采用云厂商的镜像仓储系统，还需要登陆云厂商的系统去查看镜像信息）的地址，更不用说加入安全扫描等操作。这种情况增加了开发人员的工作负担，他们不仅需要记录这些地址，还需要对所有的系统或者工具有所了解，如果系统或者工具发生变更，重复的操作还要再来一边。对于开发人员来说，能在 GitLab 上完成开发所需的所有内容，开发体验提升了，效率自然而然也就提高了（使用自己熟悉而且喜欢的工具，工作起来总是很舒服）。

![gitlab1](https://github.com/majinghe/DevOps/blob/main/images/gitlab-3.png)


### 合规审计变得容易

GitLab 将作为所有操作（代码变更、镜像构建、安全测试等）的统一入口，相关的操作都会有相应的记录，可以看到哪些人员在哪些时候对哪些项目做了哪些操作，一目了然，所见即所得。这就让合规审计变得简单。


### 提高了安全性

当使用多种工具来完成软件开发时，针对每个用户都需要对不同工具做权限管理，尤其当我们选择一些自身并不带权限管理的工具时，权限管理就变成了一个比较头疼的事情。而 GitLab 是一个一体化，它会作为相关人员权限管理（鉴权/授权，Authentication/authorization）的唯一入口，能够对相应人员做到细粒度的权限管理。安全性就得到了一定程度的提高。

当然，使用的好处需要用户亲自体验。


## GitLab 最大不同是什么。

上面说了那么多，那么 GitLab 和现在市面上众多的一体化DevOps 平台（或者研发效能平台）有什么不同呢？

最大的不同就在于极狐 GitLab 是**open source**，也就是**开源**的，而且是**open core**，也即**核心开放**。

软件吞噬世界，开源吞噬软件。开源势必会成为软件开发的新趋势和风向标。更多关于开源及 GitLab 是如何做到 open core 的，可以参考过往文章。


## 写在最后

来来来，敲黑板总结一下今天的极狐 GitLab 之初探秘：

* GitLab 不仅仅是一个代码托管平台
* GitLab 是一个一体化DevOps 平台
* GitLab 是开源的，坚持核心开放，人人共享

敬请期待后续的探秘文章，我们将逐一揭秘上述的功能内容那个是如何具体实践的。
