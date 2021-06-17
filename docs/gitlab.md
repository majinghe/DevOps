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


