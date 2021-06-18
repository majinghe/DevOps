# GitLab —— 一个酸爽的一站式 DevOps 平台

## 写在最前

重要的话要说在、写在最前面，而且应该是多遍：**GitLab 不仅仅是一个代码托管平台，而且一个一站式的 DevOps 平台。它是一个平台，关于 DevOps 的，而且最最重要的是它是一站式的。**

![gitlab](https://github.com/majinghe/DevOps/blob/main/images/radar.png)


不信？先看看 [CNCF 持续交付技术雷达](https://radar.cncf.io/2020-06-continuous-delivery)。众所周中，持续交付（Continuous Delivery）是 DevOps 实践的核心关键能力，也是各个企业或者组织积极推进 DevOps 落地所追求的目标。从技术雷达看，GitLab 赫然在列，而且在 TRIAL 阶段。足以佐证最开始的阐述：**GitLab 不仅仅是一个代码托管平台，它还是关于 DevOps 的一个平台**，至于是怎样的一个平台，看完下面的内容，相信你会有自己的判断。

## GitLab 揭秘

DevOps 出现也有十多年了，最近几年呈火爆的发展趋势，我们可以先不用管 GitLab 有什么，先想想我们如果要推进 DevOps 落地的话，我们会关心哪些问题。

### 代码托管

代码毫无疑问是我们最看重的，也是我们 IT“打工人”在经历 996/007 福报之后的智慧结晶。代码托管也是 GitLab 最基本的功能之一，分支管理（branch）、代码审查（review）、代码合并（merge）等都是一应俱全。熟悉 Git 操作的小伙伴可以很快上手 GitLab。 


### CI/CD

CI/CD（continuous integration/continuous deployment(delivery)) 是 **DevOps 落地实践的两大核心关键能力**。甚至有很多企业或者组织认为实现了 CI/CD 就等于落地了 DevOps。可见 CI/CD 的重要性。GitLab 同样提供了出色的 CI/CD 功能，比如说只需要简单的配置一下 `.gitlab-ci.yml` 文件，就可以体验 CI/CD 功能。如下所示，就是一个输出“Hello World”的配置文件示例。（“Hello World 是程序员认知世界万物的开始）
```
job:
  script:
    - echo "Hello World, This is GitLab"
```

> 当然，CI/CD 的使用要从托管项目的实际出发，书写并调试正确的配置文件。

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
### 安全相关



## GitLab 最大不同是什么。

Open Source



## 一站式 DevOps 有什么好处


### 提升开发体验

这一点就像大家去万达一样，购物、娱乐、餐饮应有尽有，消费者不用出万达商城就能满足一切需求，省去了大家在不同地点来回折腾的烦恼。GitLab 的一站式 DevOps 平台提供了用户的所有需求，用户只需要在这一个平台就能完成所有操作，不用在构建时切到构建工具的地址，镜像扫描切到镜像系统（上云的用户一般采用云厂商的镜像仓储系统，还需要登陆云厂商的系统去查看镜像信息）的地址，更不用说加入安全扫描等操作。这种情况增加了开发人员的工作负担，他们不仅需要记录这些地址，还需要对所有的系统或者工具有所了解，如果系统或者工具发生变更，重复的操作还要再来一边。对于开发人员来说，能在 GitLab 上完成开发所需的所有内容，开发体验提升了，效率自然而然也就提高了（使用自己熟悉而且喜欢的工具，工作起来总是很舒服）。

![gitlab1](https://github.com/majinghe/DevOps/blob/main/images/gitlab.png)


### 合规审计变得容易



### 提高了安全性


## GitLab 最大不同是什么。

上面说了那么多，那么 GitLab 和现在市面上众多的一站式 DevOps 平台（或者研发效能平台）有什么不同呢？

最大的不同就在于 GitLab 是**open source**，也就是**开源**的，而且是**open core**，也即**核心开放**。

软件吞噬世界，开源吞噬软件。开源势必会成为软件开发的新趋势和风向标。更多关于开源及极狐 GitLab 是如何做到 open core 的，可以参考过往文章。


## 写在最后

来来来，敲黑板总结一下今天的极狐 GitLab 之初探秘：

* GitLab 不仅仅是一个代码托管平台
* GitLab 是一个一站式 DevOps 平台
* GitLab 不是有什么给你什么，而是你要什么就有什么
* GitLab 是开源的，坚持核心开放，人人共享

敬请期待后续的探秘文章，我们将逐一揭秘上述的功能内容那个是如何具体实践的。
