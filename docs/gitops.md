## 技术与标准 ｜ GitOps 与 OGA

### GitOps：又一次造词运动？

伴随着 DevOps 在近些年的火爆，围绕 xOps 产生了很多概念，诸如 DevSecOps，AIOps，MLOps，ChatOps 等等，当然还有今天讲述的主角 GitOps。人们在 xOps 这条造词之路上越走越远，也从“一环”（Ops）到了“二环”（DevOps，AIOps，ChatOps 等）再到了“三环”（DevSecOps，DevBizOps GitSecOps 等），“四环”在等待大家一起创造修建。

![xops](https://github.com/majinghe/DevOps/blob/main/images/gitops/xops.png)

诚然，“造词运动”产生的概念让人们目不暇接，每一个点都意味着有新东西出来，让本来就不够用的脑容量更加捉襟见肘，唯有“躺平”以应对。但是，就算“躺平”也要积极的“躺平”，学习完 GitOps 之后躺下慢慢平复 GitOps 带来的激动心情。

GitOps 的出现与云计算的大力推进有关，准确点，大胆点说与**云原生**有关。

### 大名鼎鼎的云原生（Cloud Native）

现如今，没听过云原生都不好意思跟别人交流，不知道云原生都没法跟别人说组织在上云。云原生概念的提出在 2013 年，经过了这几年的演进，成立了发展势头火爆的 CNCF（Cloud Native Computing Foundation）基金会，也对与云原生的定义，有了一个大家都接受的定义：

云原生技术使企业能够在现代动态环境中构建和运行可扩展的应用程序，如公共云、私有云和混合云。容器、服务网、微服务、不可变的基础设施和声明式的API就是这种方法的典范。

> Cloud native technologies empower organizations to build and run scalable applications in modern, dynamic environments such as public, private, and hybrid clouds. Containers, service meshes, microservices, immutable infrastructure, and declarative APIs exemplify this approach.
