# 第一部分：DevOps概述

## CI/CD

* 持续集成(Continuous Integration， CI)
持续集成是指将开发人员的代码频繁的向主干分支集成的过程，其目的在于将代码变更可能造成的系统破坏性降到最小，一旦有问题，也能够快速的识别和隔离变更集。保证主干分支实时可用。

![](https://github.com/lhb008/DevOps/blob/main/images/devops-ci.jpg)

* 持续交付(Continuous Delivery，CD)
是一组通用的软件工程原则，允许通过使用自动化测试和持续集成频繁的发布软件新版本。
![](https://github.com/lhb008/DevOps/blob/main/images/devops-cd.jpg)
* 持续部署(Continuous Deployment，CD)
持续部署是通过定义测试和验证来将风险最小化， 从而将变更部署到生产环境中。
![](https://github.com/lhb008/DevOps/blob/main/images/devops-cde.jpg)
> 持续交付和持续部署看起来都是将变更及时部署到生产环境中，但是他们是有差别的，持续交付通常被认为是持续集成的更进一步，不只是确保可以集成新变更而不会导致回归到自动化测试，它还意味着可以部署这些变更。持续交付可以确保部署新变更，持续部署则表示将这些变更真正的部署到生产环境中。另外，Jez Humble在 《持续交付》一书中提到，持续交付可以适用于任何软件开发项目，包括物联网和嵌入式项目，但是持续部署则特定于Web软件。

## Blue/Green deployment(蓝绿部署)

![](https://github.com/lhb008/DevOps/blob/main/images/blue-green.jpg)

> 蓝绿部署和 A/B Testing的区别在于，蓝绿部署的目的是为了能够使产品新版本的发布可控、稳定；而A/B测试则侧重于对于产品的功能测试。


## Canary deployment（灰度发布）
![](https://github.com/lhb008/DevOps/blob/main/images/canary.jpg)
