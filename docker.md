## 虚拟化技术的发展

![](https://github.com/majinghe/DevOps/blob/main/images/container-history.png)

## docker 概述
### 什么是 docker
* 是一家公司
* 是一种虚拟化技术
* 是一个容器
* 将应用程序和运行时环境进行打包封装(host, runtime, code, operating system, tools, libraries)，实现了 **build once, running anywhere**。

### docker 的核心概念
* 镜像
* 镜像仓库
* Dockerfile
* 容器

### docker 的架构
![](https://github.com/majinghe/DevOps/blob/main/images/docker-arch.png)

## docker 的使用

### 常规应用部署

* Step 1 写代码
```
package main

import (
    "fmt"
    "log"
    "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello DevOpsDay, this is xiaomage")
}

func main() {
    http.HandleFunc("/", handler)
    log.Fatal(http.ListenAndServe(":9999", nil))
}
```

* Step 2 安装测试环境

需要确保环境安装了合适版本的运行环境`GO`。

* Step 3 启动运行

```
go main.go
```

* Step 4 测试应用

打开浏览器的 `localhost:9999`，查看输出内容

![](https://github.com/majinghe/DevOps/blob/main/images/check.png)

如果开发测试完毕，就继续其他环境的安装、部署和测试工作。其实是上面 2、3、4 步的重复工作。这其中会带来以下几个问题：

* 环境漂移（无法保证所有测试环境的一致性）
* 应用程序运行环境的维护繁琐（安装、升级甚至回退）
* 迁移成本高（需要 clone 环境）

### 使用 docker 来部署

* Step 1 编写代码（同上）
* Step 2 编写 `Dockerfile`

```
FROM golang:1.12.9-alpine3.9

MAINTAINER <devops008@sina.com>

WORKDIR /usr/src/app/

COPY main.go /usr/src/app

CMD ["go","run", "main.go"]
```
* Step 3 构建镜像并推送至镜像仓库

[![Build Docker Image](https://asciinema.org/a/6JPchmyFPnoetUUc7HJnZc7qh.svg)](https://asciinema.org/a/6JPchmyFPnoetUUc7HJnZc7qh)

* 部署应用

使用如下部署应用
```
$ docker run --rm -p 9999:9999 dllhb/docker-share:v0.3
```
然后可以在浏览器中输入 `localhost:9999` 查看应用。或者用如下的命令行查看结果

```
$ curl localhost:9999
Hello DevOpsDay, this is xiaomage
```


