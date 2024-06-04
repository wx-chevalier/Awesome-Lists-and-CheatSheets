![image](https://user-images.githubusercontent.com/5803001/45699770-5d0a0f00-bb9d-11e8-8ce7-82650bfcbb39.png)

> 📖 节选自 [Awesome CheatSheet/Docker CheatSheet](https://parg.co/o9d)，对来自[官方文档](https://docs.docker.com/)及 [Docker Links](https://parg.co/o90) 中链接内容的归档整理，包含了日常工作中常用的 Docker 概念与命令，如果对于 Linux 常用操作尚不熟悉的可以参考 [Linux Commands CheatSheet](https://parg.co/oiT)。

# Docker CheatSheet | Docker 配置与实践清单

容器是在操作系统中建立隔离上下文的一种方法。实际上，这意味着它们中的每一个都有一个单独的包含了一组已安装的软件和相关配置的虚拟文件系统。由于它们是相互隔离的，因此任何容器都不能直接访问或影响其他容器或底层宿主操作系统。Docker 是一个开源的应用容器引擎，基于 Go 语言 并遵从 Apache2.0 协议开源。Docker 可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上。

![image](https://user-images.githubusercontent.com/5803001/43813144-f630ba5c-9af6-11e8-8443-175666d4615a.png)

虚拟机最大的瓶颈在于其需要特殊硬件虚拟化技术支持，并且携带完整的操作系统；而 Docker 没有硬件虚拟化，可以运行在物理机、虚拟机, 甚至嵌套运行在 Docker 容器内，并且其不携带操作系统的，会轻巧很多。在调用宿主机的内存、CPU、磁盘等等资源时，虚拟机是利用 Hypervisor 去虚拟化内存，整个调用过程是虚拟内存->虚拟物理内存->真正物理内存，但是 Docker 是利用 Docker Engine 去调用宿主的的资源，这时候过程是虚拟内存->真正物理内存。

Docker 综合运用了 Cgroup, Linux Namespace，Secomp capability, Selinux 等机制，在 [Docker Internals CheatSheet](./Docker-Internals-CheatSheet) 中我们会有详细的讨论，或者前往 [Backend Boilerplate/docker](https://github.com/wx-chevalier/Backend-Boilerplate/tree/master/docker) 浏览常见服务/应用的 Docker 配置案例。

![image](https://user-images.githubusercontent.com/5803001/44158672-dec2d480-a0e7-11e8-9f50-ce83c9638853.png)

# 安装与配置

## Docker CE

这里我们使用[科大的 Docker CE 源](https://mirrors.ustc.edu.cn/help/docker-ce.html)进行安装：

```sh
# 更改 Ubuntu 默认源地址
$ sudo sed -i 's/archive.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list

# 安装必备的系统命令
$ sudo apt-get install -y python-software-properties

$ curl -fsSL https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu/gpg | sudo apt-key add -

$ sudo add-apt-repository "deb [arch=amd64] https://mirrors.ustc.edu.cn/docker-ce/linux/ubuntu $(lsb_release -cs) stable"

$ sudo apt-get update

$ apt-cache policy docker-ce # 列举 docker-ce 版本

$ apt-get install docker-ce=17.03.2-ce....
```

## Daemon Configuration

```sh
# 配置开机自启动
$ sudo systemctl enable docker

# 取消开机自启动
$ sudo systemctl disable docker
```

我们还需要修改存储路径，指定镜像存储地址，允许远程访问；此时我们可以修改 systemd 中的配置文件，也可以修改 `/etc/docker/daemon.json`，此处以修改服务为例：

```sh
# 使用 systemctl 命令行修改
$ sudo systemctl edit docker.service

# 或者查找配置地址并使用 Vim 修改
$ systemctl status docker

# 修改文件内容
[Service]
ExecStart=
ExecStart=/usr/bin/dockerd -H fd:// -H tcp://127.0.0.1:2375 -H unix:///var/run/docker.sock --insecure-registry 10.196.108.176:5000 --dns 114.114.114.114 --dns 8.8.8.8 --dns 8.8.4.4 -g /mnt
```

然后重启服务：

```sh
# 重新载入服务配置
$ sudo systemctl daemon-reload

# 重启 Docker
$ sudo systemctl restart docker.service

# 判断是否配置成功
$ sudo netstat -lntp | grep dockerd
```

## Docker Swarm

```sh
# 在主节点启动 Swarm
$ docker swarm init

# 查看 Swarm 密钥
$ docker swarm join-token -q worker

# 在主节点启动 Procontainer
$ docker run -it -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock portainer/portainer

# 在主节点启动 Registry
$ docker run -d -p 5000:5000 --restart=always --name registry registry:2

# 将子节点加入到 Swarm
$ docker swarm join \
--token ${TOKEN} \
10.196.108.176:2377
```

## 常用配置

### 代理

鉴于 gcr 域名的不可用，我们需要利用 [ss-privoxy](https://hub.docker.com/r/bluebu/shadowsocks-privoxy/) 等工具搭建 Docker 源代理，也可以参考[这里](https://www.jianshu.com/p/13f4b23824d8)手动配置客户端：

```sh
$ docker run -i -t -e SERVER_ADDR=ss.server.ip -e SERVER_PORT=port -e PASSWORD=123456 bluebu/shadowsocks-privoxy
```

如果需要手动安装，需要先安装 sslocal 命令：

```sh
$ apt install python3-pip
$ pip3 install https://github.com/shadowsocks/shadowsocks/archive/master.zip -U
```

写入你的配置文件到例如 `config.json`：

```json
{
    "server": "...",
    "server_port": ...,
    "local_port": 1080,
    "password": "..."
    "method": "chacha20-ietf-poly1305",
    "timeout": 600
}
```

启动：

```sh
$ sslocal -c config.json
```

这时一个 socks5 代理在你本机就启动了。下面安装配置 privoxy 把他转成 http/https 代理。安装略。修改/添加两个 privoxy 的配置(对于 ubuntu, 在 /etc/privoxy/config)：

```
listen-address 0.0.0.0:8118        # 所有 interface 上监听流量
forward-socks5 / 127.0.0.1:1080 .  # 流量导向本机上的 ss 代理
```

这时可以访问一下不存在的网站测试一下：

```
HTTP_PROXY=127.0.0.1:8118 HTTPS_PROXY=127.0.0.1:8118 curl https://www.google.com
```

下面修改各台机器的 docker 配置(假定我们的 master 内网地址 `1.1.1.2`, 其他两台机器地址为 `1.1.1.3` 和 `1.1.1.4`)：

```
[Environment]
Environment="HTTP_PROXY=127.0.0.1:8118" "HTTPS_PROXY=127.0.0.1:8118" "NO_PROXY=localhost,127.0.0.1,1.1.1.2,1.1.1.3,1.1.1.4"

...
```

环境变量 `NO_PROXY` 顾名思义，它不支持 CIDR 应该，所以需要你枚举一下集群主机地址。

### 存储与日志

线上系统中我们往往也需要对于 Docker 产生的

# 镜像

镜像描述了 Docker 容器运行的初始文件系统, 包含运行应用所需的所有依赖。即可以是一个完整的操作系统, 也可以仅包含应用所需的最小 bin/lib 文件集合。Docker 镜像和容器采用分层文件系统结构, 每个容器包含一层薄薄的可写层, 只读部分是共享的，这种机制保证了资源的可复用性，减少了镜像与容器的空间占用。Docker 镜像存储引擎有 aufs, devicemapper, overlay 等多种实现。

## 构建与拉取

编写完成 Dockerfile 之后，可以通过 `docker build` 命令来创建镜像；关于 Dockfile 的具体语法，可以查看下文。Dockfile 基本的格式为 `docker build [ 选项 ] 路径`，该命令将读取指定路径下(包括子目录)的 Dockerfile，并将该路径下所有内容发送给 Docker 服务端，由服务端来创建镜像。因此一般建议放置 Dockerfile 的目录为空目录。也可以通过 `.dockerignore` 文件(每一行添加一条匹配模式)来让 Docker 忽略路径下的目录和文件。

镜像的完整 tag 不仅包含镜像名字, 还指明了镜像从哪里来, 要到哪里去, 就像一个 URL。可以通过 `-t` 选项指定镜像的标签信息，譬如：

```sh
$ sudo docker build -t myrepo/myapp /tmp/test1/

$ docker build -t username/image_name:tag_name .

$ docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]
```

Docker 支持从 Registry 拉取镜像，或者将某个容器保存为镜像：

```sh
# 拉取镜像
$ docker pull image_name

# 将某个容器保存为镜像
$ docker commit -m “commit message” -a “author”  container_name username/image_name:tag
```

Docker 支持将镜像保存为文件，以方便镜像的导出与加载：

```sh
# 保存镜像
$ docker save --output saved-image.tar my-image:1.0.0
$ docker save my-image:1.0.0 > saved-image.tar
$ docker save my_image:my_tag | gzip > my_image.tar.gz

# 导入镜像
$ docker load --input saved-image.tar
$ docker load < saved-image.tar
```

## 镜像管理

`docker images` 命令会列举出全部的镜像:

```
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
mynewimage          latest              4d2eab1c0b9a        5 minutes ago       278.1 MB
ubuntu              14.04               ad892dd21d60        11 days ago         275.5 MB
<none>              <none>              6b0a59aa7c48        11 days ago         169.4 MB
<none>              <none>              6cfa4d1f33fb        7 weeks ago         0 B
```

Docker 中镜像主要分为三种状态:

- 已使用镜像(used image): 指所有已被容器（包括已停止的）关联的镜像。即 docker ps -a 看到的所有容器使用的镜像。
- 未引用镜像(unreferenced image): 没有被分配或使用在容器中的镜像，但它有 Tag 信息。
- 悬空镜像(dangling image): 未配置任何 Tag（也就无法被引用）的镜像，所以悬空。这通常是由于镜像 build 的时候没有指定 -t 参数配置 Tag 导致的。

```sh
# 列举未使用的
$ docker images --filter "dangling=true"

# 删除所有无用的镜像
$ docker rmi $(docker images -q -f dangling=true)
```

## Dockfile

Dockerfile 由一行行命令语句组成，并且支持以 `#` 开头的注释行。一般的，Dockerfile 分为四部分：基础镜像信息、维护者信息、镜像操作指令和容器启动时执行指令；指令的一般格式为 `INSTRUCTION arguments`，指令包括 `FROM`、`MAINTAINER`、`RUN` 等。例如：

```sh
#
# MongoDB Dockerfile
#
# https://github.com/dockerfile/mongodb
#

# Pull base image.
FROM dockerfile/ubuntu

ENV SOURCE http://downloads-distro.mongodb.org/repo/ubuntu-upstart

# Install MongoDB.
RUN \
  apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 7F0CEB10 && \
  echo 'deb $SOURCE dist 10gen' > /etc/apt/sources.list.d/mongodb.list && \
  apt-get update && \
  apt-get install -y mongodb-org && \
  rm -rf /var/lib/apt/lists/*

ENV PATH /usr/local/mongo/bin:$PATH

# Define mountable directories.
VOLUME ["/data/db"]

# Define working directory.
WORKDIR /data

# Define default command.
CMD ["mongod"]

# Expose ports.
#   - 27017: process
#   - 28017: http
EXPOSE 27017
EXPOSE 28017
```

其中，一开始必须指明所基于的镜像名称，接下来推荐说明维护者信息。后面则是镜像操作指令，例如 `RUN` 指令，`RUN` 指令将对镜像执行跟随的命令。每运行一条 `RUN` 指令，镜像添加新的一层，并提交。最后是 `CMD` 指令，来指定运行容器时的操作命令。

| 指令名     | 格式                                                                                                                                                                                                              | 描述                                                                                                                                                                         | 备注                                                                                                      |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| FROM       | 格式为 `FROM <image>`或`FROM <image>:<tag>`                                                                                                                                                                       | 第一条指令必须为 `FROM` 指令                                                                                                                                                 | 如果在同一个 Dockerfile 中创建多个镜像时，可以使用多个 `FROM` 指令(每个镜像一次)                          |
| MAINTAINER | 格式为 `MAINTAINER <name>`                                                                                                                                                                                        | 指定维护者信息，                                                                                                                                                             |
| RUN        | `RUN <command>`或`RUN ["executable", "param1", "param2"]`                                                                                                                                                         | 前者将在 shell 终端中运行命令，即 `/bin/sh -c`；后者则使用 `exec` 执行。指定使用其它终端可以通过第二种方式实现，例如 `RUN ["/bin/bash", "-c", "echo hello"]`                 | 每条 `RUN` 指令将在当前镜像基础上执行指定命令，并提交为新的镜像。当命令较长时可以使用 `\` 来换行，        |
| CMD        | 支持三种格式,`CMD ["executable","param1","param2"]` 使用 `exec` 执行，推荐方式；`CMD command param1 param2` 在 `/bin/sh` 中执行，提供给需要交互的应用；`CMD ["param1","param2"]` 提供给 `ENTRYPOINT` 的默认参数； | 指定启动容器时执行的命令，每个 Dockerfile 只能有一条 `CMD` 命令。如果指定了多条命令，只有最后一条会被执行。如果用户启动容器时候指定了运行的命令，则会覆盖掉 `CMD` 指定的命令 |
| EXPOSE     | `EXPOSE <port> [<port>...]`                                                                                                                                                                                       | 告诉 Docker 服务端容器暴露的端口号，供互联系统使用                                                                                                                           | 在启动容器时需要通过 -p 来指定端口映射，Docker 主机会自动分配一个端口转发到指定的端口                     |
| ENV        | `ENV<key><value>`。指定一个环境变量，会被后续 `RUN` 指令使用，并在容器运行时保持                                                                                                                                  |                                                                                                                                                                              |
| ADD        | `ADD<src><dest>`                                                                                                                                                                                                  | 该命令将复制指定的 `<src>` 到容器中的 `<dest>`，                                                                                                                             | `<src>` 可以是 Dockerfile 所在目录的一个相对路径；也可以是一个 URL；还可以是一个 tar 文件(自动解压为目录) |
| COPY       | `COPY <src><dest>`                                                                                                                                                                                                | 复制本地主机的 `<src>`(为 Dockerfile 所在目录的相对路径)到容器中的 `dest`                                                                                                    | 当使用本地目录为源目录时，推荐使用 `COPY`                                                                 |
| ENTRYPOINT | `ENTRYPOINT ["executable", "param1", "param2"]`，使用指定可执行文件执行；`ENTRYPOINT command param1 param2`，会在 Shell 中执行                                                                                    | 配置容器启动后执行的命令，并且不可被 `docker run` 提供的参数覆盖。每个 Dockerfile 中只能有一个 `ENTRYPOINT`，当指定多个时，只有最后一个起效，                                |
| VOLUME     | `VOLUME ["/data"]`                                                                                                                                                                                                | 创建一个可以从本地主机或其他容器挂载的挂载点，一般用来存放数据库和需要保持的数据等                                                                                           |
| USER       | `USER daemon`                                                                                                                                                                                                     | 指定运行容器时的用户名或 UID，后续的 `RUN` 也会使用指定用户                                                                                                                  |                                                                                                           |
| WORKDIR    | `WORKDIR /path/to/workdir`                                                                                                                                                                                        | 为后续的 `RUN`、`CMD`、`ENTRYPOINT` 指令配置工作目录                                                                                                                         | 可以使用多个 `WORKDIR` 指令，后续命令如果参数是相对路径，则会基于之前命令指定的路径                       |

当服务不需要管理员权限时，可以通过该命令指定运行用户。并且可以在之前创建所需要的用户，例如：`RUN groupadd -r postgres && useradd -r -g postgres postgres`；要临时获取管理员权限可以使用 `gosu`，而不推荐 `sudo`。

RUN、CMD 和 ENTRYPOINT 这三个 Dockerfile 指令看上去很类似，很容易混淆。RUN 执行命令并创建新的镜像层，RUN 经常用于安装软件包。CMD 设置容器启动后默认执行的命令及其参数，但 CMD 能够被 docker run 后面跟的命令行参数替换。ENTRYPOINT 配置容器启动时运行的命令。我们经常可以使用 ENTRYPOINT 指定固定命令，使用 CMD 动态传入参数。

```Dockerfile
ENTRYPOINT ["/bin/echo", "Hello"]
CMD ["world"]

# docker run -it <image>
# Hello world
# docker run -it <image> John
# Hello John
```

Docker 推荐的是单个容器执行单个任务的关注点分离策略，容器的主进程会负责管理所有的子进程。如果我们未在自定义初始化脚本中考虑太多子进程生命周期管理的操作，那么可以使用 `--init` 参数来允许 Docker 自动注入 init 进程作为主进程，其会在容器关闭时候自动处理所有的派生的子进程，并且相对于完整的 sysvinit 或者 systemd 更为轻量级。如果我们希望在单个容器中运行多个进程，则可以使用 supervisord 或者[自定义脚本](https://docs.docker.com/config/containers/multi-service_container/):

```Dockerfile
FROM ubuntu:latest
RUN apt-get update && apt-get install -y supervisor
RUN mkdir -p /var/log/supervisor
COPY supervisord.conf /etc/supervisor/conf.d/supervisord.conf
COPY my_first_process my_first_process
COPY my_second_process my_second_process
CMD ["/usr/bin/supervisord"]
```

## Registry

Docker 允许我们建立私有的 Registry 来存放于管理镜像，直接运行如下命令即可创建私有 Registry：

```sh
$ docker run -d -p 5000:5000 --restart=always --name registry registry:2
```

参考上文描述我们可知，镜像名的前缀即表示该镜像所属的 Registry 地址，因此我们可以通过 tag 方式将某个镜像推送到私有仓库：

```sh
# 拉取公共镜像
$ docker pull ubuntu:16.04

# 为镜像添加 Registry 信息
$ docker tag ubuntu:16.04 custom-domain:5000/my-ubuntu

# 将其推送到私有镜像库
$ docker push custom-domain:5000/my-ubuntu

# 从私有镜像库中拉取镜像
$ docker pull custom-domain:5000/my-ubuntu
```

我们也可以指定镜像库的存放地址：

```sh
-v /mnt/registry:/var/lib/registry
```

很多情况下我们的内部仓库并不会配置 HTTPS，如果希望以 HTTP 方式访问，那么需要在任何需要推送/拉取镜像的机器上配置非安全域名：

```json
{ "insecure-registries": ["myregistry.example.com:5000"] }
```

有时候我们也需要为私有仓库配置权限认证，那么首先需要添加 TLS 支持，并且配置认证文件：

```sh
$ mkdir auth
$ docker run \
  --entrypoint htpasswd \
  registry:2 -Bbn cscan cscancscan > ~/auth/htpasswd

$ openssl req -new -newkey rsa:4096 -days 365 \
                -subj "/CN=localhost" \
                -nodes -x509  \
                -keyout ~/certs/domain.key \
                -out ~/certs/domain.crt
```

然后可以使用 Compose 文件来描述所需要的 TLS 以及 AUTH 参数：

```yml
registry-srv:
  restart: always
  image: registry:2
  ports:
    - 5000:5000
  environment:
    REGISTRY_HTTP_TLS_CERTIFICATE: /certs/domain.crt
    REGISTRY_HTTP_TLS_KEY: /certs/domain.key
    REGISTRY_AUTH: htpasswd
    REGISTRY_AUTH_HTPASSWD_PATH: /auth/htpasswd
    REGISTRY_AUTH_HTPASSWD_REALM: Registry Realm
  volumes:
    - /opt/registry:/var/lib/registry
    - ~/certs:/certs
    - ~/auth:/auth
```

接下来使用 Docker Compose 命令启动服务：

```sh
$ docker-compose up -d

# 登录到镜像服务器
$ docker login myregistrydomain.com:5000
```

## 多阶段构建

随着 17.05 版本的发布，Docker 对于镜像构建这块也作了一项重要更新，那就是 multi-stage build（多阶段构建），这有助于方便源代码控制，减小镜像体积。

```Dockerfile
# First stage: complete build environment
FROM maven:3.5.0-jdk-8-alpine AS builder
# add pom.xml and source code
ADD ./pom.xml pom.xml
ADD ./src src/
# package jar
RUN mvn clean package

# Second stage: minimal runtime environment
From openjdk:8-jre-alpine
# copy jar from the first stage
COPY --from=builder target/msb-1.0.jar msb.jar
# run jar
CMD ["java", "-jar", "msb.jar"]
```

对于 multi-stage build，其关键点主要有两点：

在前面阶段的 FROM 指令后面增加了一个 AS 参数，可为该构建阶段命名，便于后续构建阶段引用，格式如下：

```
FROM image[:tag | @digest] AS stage
```

在后续阶段的 COPY 指令后面增加了--from 参数，指明引用前面哪一个构建阶段的成果，格式如下：

```
COPY --from=stage ...
```

同理，多阶段构建同样可以很方便地将多个彼此依赖的项目通过一个 Dockerfile 就可轻松构建出期望的容器镜像，而不用担心镜像太大、源码泄露等风险。

# 容器

Docker 中镜像是只读的, 创建容器时只是在镜像上面新建一个可写层, 不需要复制整个文件系统, 因而可以实现毫秒级创建。

![image](https://user-images.githubusercontent.com/5803001/45262735-4f42e400-b44f-11e8-96a0-79c305006be8.png)

## 启停控制

- `docker create`: 创建一个容器但是不启动。
- `docker rename`: 允许重命名容器。
- `docker run`: 在同一个操作中创建并启动一个容器。
- `docker rm`: 删除容器。
- `docker update`: 更新容器的资源限制。

容器会在结束命令之后自动退出，使用以下的命令选项可以将容器保持在激活状态：

- `-i` 即使在没有附着的情况下依然保持 STDIN 处于开启。单纯使用 -i 命令是不会出现 `root@689d580b6416:/` 这种前缀

- `-t` 分配一个伪 TTY 控制台

```sh
# 创建，并且启动某个容器以执行某个命令
$ docker run -ti --name container_name image_name command

# 创建，启动容器执行某个命令然后删除该容器
$ docker run --rm -ti image_name command

# 创建，启动容器，并且映射卷与端口，同时设置环境变量
$ docker run -it --rm -p 8080:8080 -v /path/to/agent.jar:/agent.jar -e JAVA_OPTS=”-javaagent:/agent.jar” tomcat:8.0.29-jre8

# 创建容器，指定网络
$ docker run --network=<NETWORK>
# 直接使用宿主机的网络
$ docker run --rm -d --network host --name my_nginx nginx

# 指定标签
$ docker run -l my-label --label com.example.foo=bar ubuntu bash
```

默认情况下，创建容器时，它不会将其任何端口发布到外部世界。要使端口可用于 Docker 之外的服务或未连接到容器网络的 Docker 容器，请使用 --publish 或-p 标志。这会创建一个防火墙规则，将容器端口映射到 Docker 主机上的端口。

| 标志值                          | 描述                                                       |
| ------------------------------- | ---------------------------------------------------------- |
| `-p 8080:80`                    | 将容器的 80 端口映射到 Docker 主机的 8080 端口(TCP)        |
| `-p 8080:80/udp`                | 将容器的 80 端口映射到 Docker 主机的 8080 端口(UDP)        |
| `-p 8080:80/tcp -p 8080:80/udp` | 将容器的 80 端口映射到 Docker 主机的 8080 端口(TCP 和 UDP) |

```sh
# 启动/停止某个容器
$ docker [start|stop] container_name

# 在某个容器内执行某条命令
$ docker exec -ti container_name command.sh

# 查看某个容器的输出日志
$ docker logs -ft container_name
```

## 状态查询

- docker ps 查看运行中的所有容器。
- docker logs 从容器中获取日志。(你也可以使用自定义日志驱动，不过在 1.10 中，它只支持 json-file 和 journald)
- docker inspect 查看某个容器的所有信息(包括 IP 地址)。
- docker events 从容器中获取事件(events)。
- docker port 查看容器的公开端口。
- docker top 查看容器中活动进程。
- docker stats 查看容器的资源使用情况统计信息。
- docker diff 查看容器的 FS 中有变化文件信息。

```sh
# 根据条件过滤查询
$ docker ps --filter "name=nostalgic"

# 显示正在运行的容器列表
$ docker stats --all

# 批量查看日志
for i in $(docker ps -qf name=wsat_slave*); do echo "==================$i" && docker logs $i  | grep aisec; done
```

## 管理配置

创建容器时也可以容器的重启策略，即是当容器出错退出或者宿主机重启时候，容器的应对策略；重启策略同样会保证相关联的容器以正确的顺序重启，避免意外的错误。

- no: 不进行重启
- on-failure: 当容器以非零状态码退出时重启容器
- unless-stopped: 当某个容器被显性关闭或者 Docker 本身关闭或重启时重启
- always: 无论出现任何情况都重启容器

```sh
# 设置重启策略
# Off, On-failure, Unless-stopped, Always
$ docker run -dit — restart unless-stopped [CONTAINER]
```

可以通过多种过滤条件来进行容器的移除：

```sh
# 关闭所有正在运行的容器
$ docker kill $(docker ps -q)

# 批量重启容器
$ docker restart $(docker ps -a -q)

# 根据 ID或Name 移除
$ docker rm idOrName

# 移除所有停止的容器
$ docker rm $(docker ps -a -q)

# 根据状态移除
$ docker rm $(docker ps -q -f 'status=exited')

# 根据标签移除
$ docker rm $(docker ps -a | grep rabbitmq | awk '{print $1}')
$ docker rm $(docker ps -a | grep "46 hours ago")
```

我们也可以对容器中的文件进行导入导出操作:

- docker cp 在容器和本地文件系统之间复制文件或文件夹。
- docker export 将容器的文件系统切换为压缩包(tarball archive stream)输出到 STDOUT。

## 资源配额

我们可以使用 `docker stats` 命令来查看 Docker 容器的性能状态与资源占用:

```sh
$ docker stats redis1 redis2

CONTAINER           CPU %               MEM USAGE / LIMIT     MEM %               NET IO             BLOCK IO
redis1              0.07%               796 KB / 64 MB        1.21%               788 B / 648 B       3.568 MB / 512 KB
```

### Memory

```sh
$ docker run -it -m 300M ubuntu:14.04 /bin/bash
```

### CPU

在线上环境中，我们即希望能够尽量避免 CPU 空间时间片，最大化资源利用率，也要保障重点业务的资源占用，避免因某个异常容器占用或不合理使用整机 CPU 资源，造成宿主机上大量容器异常；此时单容器的 CPU 资源约束及上限将变得非常重要，既不能限得太死，又不能限不住，将通过内核和调度系统的限制机制来保障资源稳定性。Docker 允许使用 cpus, cpuset-cpus, cpu-shares 等来限制容器的计算资源占用：

```sh
# 指定容器可占用的 CPU 核编号，0-3 表示占用四个核，1,3 表示占用两个核
$ docker run -it --cpuset-cpus="1,3" ubuntu /bin/bash

# 最多允许占用单 CPU 50% 的计算资源，如果双核 CPU，则可以设置为 1.5 等
$ docker run -it --cpus=".5" ubuntu /bin/bash

# 不同的值能够指定不同的容器权重，用于动态分配 CPU 资源
$ docker run -it --cpu-shares="512" ubuntu /bin/bash
```

- CPU Set 保障了容器的 CPU 核数，安全性较强，但是整体资源利用率低。如果容器实际并不需要如此多核的 CPU 资源来处理任务则会造成资源浪费，并且导致其他容器上的任务无法利用该容器上的 CPU 空闲时间片，人为阻断了 CPU 闲时复用的能力。

- CPU Share 允许通过共享的方式获得 CPU 资源，不同的容器共享一定总量的 CPU 计算能力，每个容器都绑定全量核，而每个容器获取一定份额的 CPU 计算力。该模式下，每个容器的 CPU 资源分配不再以整核分配，而是可精细到 CPU 时间片份额的粒度，并且是连续的 CPU 核能力值。当整机闲时，可以让较为繁忙的业务获得整机空闲。采用 CPU 资源共享的机制，其资源隔离性没有 set 模式强，对于极个别 CPU 资源敏感型业务，有可能出现偶尔等待 CPU 时间片的情况，而影响业务稳定性。对于极少数的这类业务，我们容许继续使用 CPU set 模式。

### Storage

如果使用 Device Mapper 作为底层存储驱动，则可以通过 Docker daemon 的如下参数来全局限制单个容器占用空间的大小:

```sh
# 限制单个容器最多占用 20G 空间，将应用于任何新建容器。
$ --storage-opt dm.basesize=20G
```

如果是 btrfs 存储驱动，可使用其提供的 subvolume 功能来实现。一个容器会对应一个 subvolume。针对容器对应的 subvolume 启用并配置 quota 即可限制其磁盘空间:

```sh
$ btrfs qgroup limit -e 50G /var/lib/docker/btrfs/subvolumes/<CONTAINER_ID>
```

授予对单个设备访问权限:

```
docker run -it --device=/dev/ttyUSB0 debian bash
```

授予所有设备访问权限:

```
docker run -it --privileged -v /dev/bus/usb:/dev/bus/usb debian bash
```

# 资源配置

## Volume | 数据卷

容器运行时应该尽量保持容器存储层不发生写操作，对于数据库类需要保存动态数据的应用，其数据库文件应该保存于卷(Volume)中。为了防止运行时用户忘记将动态文件所保存目录挂载为卷，在 Dockerfile 中，我们可以事先指定某些目录挂载为匿名卷，这样在运行时如果用户不指定挂载，其应用也可以正常运行，不会向容器存储层写入大量数据。

数据卷是一个可供一个或多个容器使用的特殊目录，它绕过 UFS，可以提供很多有用的特性：

- 数据卷可以在容器之间共享和重用
- 对数据卷的修改会立马生效
- 对数据卷的更新，不会影响镜像
- 卷会一直存在，直到没有容器使用

- 数据卷的使用，类似于 Linux 下对目录或文件进行 mount。

For example,

```sh
# the following creates a tmpfs volume called foo with a size of 100 megabyte and uid of 1000.
$ docker volume create --driver local \
    --opt type=tmpfs \
    --opt device=tmpfs \
    --opt o=size=100m,uid=1000 \
    foo
```

nother example that uses nfs to mount the /path/to/dir in rw mode from 192.168.1.1:

```sh
$ docker volume create --driver local \
    --opt type=nfs \
    --opt o=addr=192.168.1.1,rw \
    --opt device=:/path/to/dir \
    foo
```

```sh
$ docker run -d \
  -it \
  --name devtest \
  -v myvol2:/app \
  nginx:latest
```

```json
"Mounts": [
    {
        "Type": "volume",
        "Name": "myvol2",
        "Source": "/var/lib/docker/volumes/myvol2/_data",
        "Destination": "/app",
        "Driver": "local",
        "Mode": "",
        "RW": true,
        "Propagation": ""
    }
],
```

Docker `-v` 标记也可以指定挂载一个本地主机的目录 / 文件到容器中去：

```sh
# 挂载目录
$ sudo docker run -d -P --name web -v /src/webapp:/opt/webapp training/webapp python app.py

# 挂载文件
$ sudo docker run --rm -it -v ~/.bash_history:/.bash_history ubuntu /bin/bash

# Docker 挂载数据卷的默认权限是读写，用户也可以通过 `:ro` 指定为只读。
$ sudo docker run -d -P --name web -v /src/webapp:/opt/webapp:ro
training/webapp python app.py
```

注意：Dockerfile 中不支持这种用法，这是因为 Dockerfile 是为了移植和分享用的。然而，不同操作系统的路径格式不一样，所以目前还不能支持。

```yaml
VOLUME /data
```

## Network | 网络

Linux 在网络栈中引入网络命名空间，将独立的网络协议栈隔离到不同的命令空间中，彼此间无法通信；Docker 利用这一特性，实现不容器间的网络隔离，并且引入 Veth 设备对来实现在不同网络命名空间的通信。Linux 系统包含一个完整的路由功能，当 IP 层在处理数据发送或转发的时候，会使用路由表来决定发往哪里。Netfilter 负责在内核中执行各种挂接的规则(过滤、修改、丢弃等)，运行在内核模式中；Iptables 模式是在用户模式下运行的进程，负责协助维护内核中 Netfilter 的各种规则表；通过二者的配合来实现整个 Linux 网络协议栈中灵活的数据包处理机制。Docker 的网络子系统采用了基于驱动的可插拔机制，其默认包含了如下驱动模式：

- `bridge`: 默认的网络驱动，常用于多个应用运行与独立容器中并且需要相互通讯的时候。
- `host`: 移除容器与 Docker 主机之间的网络隔离，直接使用宿主机所在的网络。底层与宿主机共用一个 Network Namespace，容器将不会虚拟出自己的网卡，配置自己的 IP 等，而是使用宿主机的 IP 和端口。
- `overlay`: Overlay 网络用语连接多个 Docker Daemon，保证 Docker Swarm 服务的正常运行；独立的容器与 Swarm 服务，或者不同宿主机上的容器同样能够通过 Overlay 进行通信。
- `none`: 对于指定容器禁止所有的网络通信。
- `macvlan`: Macvlan 网络会允许直接为容器分配 MAC 地址，使其作为真正的物理设备接入到宿主机所在的网络中。

我们使用 network 命令可以查看到默认的网络：

```sh
$ docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
f707aa0ef50d        bridge              bridge              local
97dd7a032d96        host                host                local
d5a1bed0b12d        none                null                local
```

桥接模式下，当 Docker 启动时，会自动在主机上创建一个 docker0 虚拟网桥，即软件交换机，在挂载到它的网口之间进行转发。同时，Docker 随机分配一个本地未占用的私有网段(在 RFC1918 中定义)中的一个地址给 docker0 接口。比如典型的 172.17.42.1，掩码为 255.255.0.0。此后启动的容器内的网口也会自动分配一个同一网段(172.17.0.0/16)的地址。

桥接模式下，创建一个 Docker 容器的时候，同时会创建了一对 veth pair 接口(当数据包发送到一个接口时，另外一个接口也可以收到相同的数据包)。这对接口一端在容器内，即 eth0；另一端在本地并被挂载到 docker0 网桥，名称以 veth 开头(例如 vethAQI2QT)。通过这种方式，主机可以跟容器通信，容器之间也可以相互通信。Docker 就创建了在主机和所有容器之间一个虚拟共享网络。

```sh
# 创建新的网络
$ docker network create --driver bridge isolated

# 指定网段，宿主机会作为默认网关
$ docker network create --driver=bridge --subnet=192.168.2.0/24 --gateway=192.168.2.10 new_subnet

# 创建时将某个容器连接到网络
$ docker run --network=isolated -itd --name=docker-nginx nginx

# 将某个运行中容器连接到某个网络，在该网络内可以通过容器名自由访问
$ docker network connect multi-host-network container1
```

### DNS

默认情况下，容器从 Docker 守护进程继承 DNS 设置，包括 /etc/hosts 和 /etc/resolv.conf。可以基于每个容器覆盖这些设置。

- -h HOSTNAME or --hostname=HOSTNAME 设定容器的主机名，它会被写到容器内的 /etc/hostname 和 /etc/hosts。但它在容器外部看不到，既不会在 docker ps 中显示，也不会在其他的容器的 /etc/hosts 看到。
- --link=CONTAINER_NAME:ALIAS 选项会在创建容器的时候，添加一个其他容器的主机名到 /etc/hosts 文件中，让新容器的进程可以使用主机名 ALIAS 就可以连接它。
- --dns=IP_ADDRESS 添加 DNS 服务器到容器的 /etc/resolv.conf 中，让容器用这个服务器来解析所有不在 /etc/hosts 中的主机名。
- --dns-search=DOMAIN 设定容器的搜索域，当设定搜索域为 .example.com 时，在搜索一个名为 host 的 主机时，DNS 不仅搜索 host，还会搜索 host.example.com。注意：如果没有上述最后 2 个选项，Docker 会默认用主机上的 /etc/resolv.conf 来配置容器。

## 空间清理

Docker 使用过程中，可能会发现宿主节点的磁盘容量持续增长，譬如 volume 或者 overlay2 目录占用了大量的空间；如果任其发展，可能将磁盘空间耗尽进而引发宿主机异常，进而对业务造成影响。Docker 的内置 df 指令可用于查询镜像(Images)、容器(Containers)和本地卷(Local Volumes)等空间使用大户的空间占用情况。而容器的占用的总空间，包含其最顶层的读写层(writable layer)和底部的只读镜像层(base image layer，read-only)，我们可以使用 `ps -s` 参数来显示二者的空间占用情况:

```sh
# 查看当前目录下的文件空间占用
$ du -h --max-depth=1 | sort

# 空间占用总体分析
$ docker system df

# 输出空间占用细节
$ docker system df -v

# 输出容器的空间占用
$ docker ps -s
```

`docker system prune` 指令能够进行自动地空间清理，其默认会清除已停止的容器、未被任何容器所使用的卷、未被任何容器所关联的网络、所有悬空镜像:

```sh
# 一并清除所有未使用的镜像和悬空镜像
$ docker system prune --all

# 列举悬空镜像
$ docker images -f dangling=true

# 删除全部悬空镜像
$ docker image prune
# 删除所有未被使用的镜像
$ docker image prune -a

# 删除指定模式的镜像
$ docker images -a | grep "pattern" | awk '{print $3}' | xargs docker rmi

# 删除全部镜像
$ docker rmi $(docker images -a -q)

# 删除全部停止的容器
$ docker rm $(docker ps -a -f status=exited -q)

# 根据指定模式删除容器
$ docker rm $(docker ps -a -f status=exited -f status=created -q)
$ docker rm $(docker ps -a | grep rabbitmq | awk '{print $1}')

# 删除全部容器
$ docker stop $(docker ps -a -q)
$ docker rm $(docker ps -a -q)

# 列举并删除未被使用的卷
$ docker volume ls -f dangling=true
$ docker volume prune

# 根据指定的模式删除卷
$ docker volume prune --filter "label!=keep"

# 删除未被关联的网络
$ docker network prune
$ docker network prune --filter "until=24h"
```

我们也可以手动指定日志文件的尺寸或者清空日志文件:

```sh
# 设置日志文件最大尺寸
$ dockerd ... --log-opt max-size=10m --log-opt max-file=3

# 清空当前日志文件
truncate -s 0 /var/lib/docker/containers/*/*-json.log
```

# 服务治理

## Docker Compose

Docker Compose 是用于定义和运行复杂 Docker 应用的工具。你可以在一个文件中定义一个多容器的应用，然后使用一条命令来启动你的应用，然后所有相关的操作都会被自动完成；简单的 Compose 文件定义如下：

```yaml
# 指定 Docker Compose 文件版本
version: "3"
services:
  web:
    # 指定从本地目录进行编译
    build: .

    # 指定导出端口
    ports:
      - "5000:5000"

    # 替换默认的 CMD 命令
    command: python app.py

    # 将本地目录绑定到容器内目录
    volumes:
      - .:/code

  redis:
    # 镜像的 ID
    image: "redis:alpine"
```

这里用到的 Python Web 应用的 Dockerfile 如下：

```Dockerfile
FROM python:3.4-alpine
ADD . /code
WORKDIR /code
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```

值得注意的是，我们在代码中直接使用服务名作为连接地址，即可访问到 Redis 数据库：

```py
cache = redis.Redis(host='redis', port=6379)
```

然后使用 docker-compose 命令启动：

```sh
# 交互式启动
$ docker-compose up

# 守护进程式启动
$ docker-compose up -d

# 查看运行情况
$ docker-compose ps

# 关闭
$ docker-compose stop

# 移除内部卷
$ docker-compose down --volumes
```

在涉及到数据存储的场景下，我们同样可以指定 docker-compose 创建命名数据卷，并将其挂载到容器中：

```yaml
version: "3.2"
services:
  web:
    image: nginx:alpine
    volumes:
      - type: volume
        source: mydata
        target: /data
        volume:
          nocopy: true
      - type: bind
        source: ./static
        target: /opt/app/static

  db:
    image: postgres:latest
    volumes:
      - "/var/run/postgres/postgres.sock:/var/run/postgres/postgres.sock"
      - "dbdata:/var/lib/postgresql/data"

volumes:
  mydata:
  dbdata:
```

如果某个数据卷天然需要映射到本地文件，则可以指定 driver 的类型为 local:

```yaml
volumes:
  wsat_etc:
    driver: local
    driver_opts:
      o: bind
      type: none
      device: /etc/wsat/
```

## Docker Swarm

Swarm 是 Docker 公司在 2014 年 12 月初发布的一套较为简单的工具，用来管理 Docker 集群，它将一群 Docker 宿主机变成一个单一的，虚拟的主机。Swarm 使用标准的 Docker API 接口作为其前端访问入口，换言之，各种形式的 Docker Client(dockerclient in go, docker_py, docker 等)均可以直接与 Swarm 通信。

Swarm Deamon 只是一个调度器(Scheduler)和路由器(Router)，Swarm 自己不运行容器，它只是接受 Docker 客户端发送过来的请求，调度适合的节点来运行容器，这意味着，即使 Swarm 由于某些原因挂掉了，集群中的节点也会照常运行，当 Swarm 重新恢复运行之后，它会收集重建集群信息。并且 Swarm 提供的路由匹配(服务发现、负载均衡、跨容器通讯)非常可靠。在单个端口上运行一个服务，Swarm 节点的任意主机都可以访问，负载均衡完全在后台实现。

![image](https://user-images.githubusercontent.com/5803001/44953944-dfbc7a00-aecd-11e8-93dc-1fe6258aafd0.png)

Swarm 在 Scheduler 节点运行容器的时候，会根据指定的策略来计算最适合运行容器的节点，目前支持的策略有：Random, Binpack, Spread。

Random 顾名思义，就是随机选择一个 Node 来运行容器，一般用作调试用。Spread 和 Binpack 策略会根据各个节点的可用的 CPU, RAM 以及正在运行的容器的数量来计算应该运行容器的节点。在同等条件下，Spread 策略会选择运行容器最少的那台节点来运行新的容器，Binpack 策略会选择运行容器最集中的那台机器来运行新的节点。

使用 Spread 策略会使得容器会均衡的分布在集群中的各个节点上运行，一旦一个节点挂掉了只会损失少部分的容器。Binpack 策略最大化的避免容器碎片化，就是说 Binpack 策略尽可能的把还未使用的节点留给需要更大空间的容器运行，尽可能的把容器运行在一个节点上面。

```sh
# 创建一个新的服务
$ docker service create \
--image nginx \
--replicas 2 \
nginx

# 更新服务
$ docker service update \
--image nginx:alpine \
nginx

# 删除服务
$ docker service rm nginx

# 缩容，而不是直接删除服务
$ docker service scale nginx=0

# 扩容
$ docker service scale nginx=5

# 列出所有的服务
$ docker service ls

# 列出一个服务的所有实例(包括服务的健康状况)
$ docker service ps nginx

# 服务的详细信息
$ docker service inspect nginx

# 增加和删除DNS
$ docker service update --dns-add 222.222.222.222 tender_hofstadter
$ docker service update --dns-rm 222.222.222.222 tender_hofstadter

# 增加和删除端口映射
$ docker service update --publish-add 80:80 xenodochial_ritchie
$ docker service update --publish-rm 80:80 xenodochial_ritchie
```

我们也可以使用 Docker Compose 的脚本来进行批次部署：

```sh
$ docker stack deploy application
```

```yaml
version: "3"
services:
  web:
    image: registry.gitlab.com/example/example # you need to use external image
    command: npm run prod
    ports:
      - 80:80
    deploy:
      replicas: 6
      update_config:
        parallelism: 2
        delay: 10s
      restart_policy:
        condition: on-failure
```
