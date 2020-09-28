### Docker比较

集群 Redis ES Hadoop 集群 费时间 费力

发布一个项目 （Redis,  MySQL , jdk, ES） 项目能不能带上环境安装打包，不能跨平台
Windwos 最后发布到 Linux!
传统 jar 运维来做

现在 开发打包部署一套流程做完！

Docker 给以上得问题，提出了解决方案！

Docker 得思想就来自集装箱

隔离 Docker 核心思想 打包装箱 每个箱子相互隔离得

Docker 通过隔离机制 

本质 所有得技术都是代码出现了一些问题 我们需要去解决 我们才去学习

Docker得历史

2010年，几个搞IT得年轻人，就在美国成立了一家公司‘Dotcloud'
做一些pass得云计算服务!  Lxc 有关容器得技术
他们将自己的技术 容器化技术 统一的简化命名  docker!

Docker 诞生的时候，没有引起行业的注意 就活不下去

开源代码

2013年 创始人 23岁 将 Docker开源！

Docker 越来越多的人 发现docker优点！火了 Docker每一个月 更新版本

2014年 4月 9日 1.0 发布

Docker 为什么这么火？ 十分轻巧

在容器出来之前 虚拟机的技术 笨重

虚拟机：在 window中 安装 一个 虚拟机软件 通过这个软件 可以虚拟一台或者多台的电脑 笨重

虚拟机 属于 虚拟化技术 Docker 是一种容器技术！

```
vm. linux centos 隔离 需要开启多个虚拟机
docker 隔离 镜像 最核心的环境 4m jdk mysql 很小巧 运行镜像就可以了 小巧 容器 几10M 容器秒级启动

```

到现在 所有开发人员都必须要学会的Docker

### 聊聊Docker
Docker是基于 Go语言的开发的 开源项目

官网地址 https://www.docker.com/

文档地址 https://docs.docker.com/ Docker文档是超级详细的!

仓库地址: https://hub.docker.com/  docker push

### Docker 能干嘛

之前虚拟器技术

缺点：
1. 资源占用十分多
2. 沉余很多
3. 启动很慢

#### 容器化技术

容器化技术不是模拟一个
比 Docker 和 虚拟机的技术不同

1.传统的虚拟机 虚拟出来硬件 运行一个玩着的操作系统 然后在这个系统 安装和运行软件

2.容器内应用直接运行在宿主机的内容 容器是没有自己的内核 但没有虚拟机虚拟我们的硬件 所以就轻便的

3.每个容器见是相互隔离的 每个容器内部有一个属于自己的文件系统，互不影响

### DevOps (开发运维)

更快速的交付和部署
传统 一堆文档 安装程序

Docker 一键运行打包镜像发布测试

#### 更便捷的升级和扩容器

使用了Docker之后，我们部署应用就和搭积木一样！

SpringBoot 1.5 Redis 5  tomcat8 升级

项目打包为一个镜像 扩展 服务器A 服务器B

#### 更简单的运维系统

在容器化之后，我们开发，测试环境高度一致的

#### 更高效的计算资源利用
1核 2g 服务器!

Docker 内核级别的 虚拟化 可以再一个物理机上可以运行很多的容器实列

服务器的性能可以压榨到极致

只要学不死 就往死里学

### Docker 安装
### Docker的基本组成

![image-20200927164421619](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200927164421619.png)

#### 镜像 （images）

docker镜像就好比是一个模板 可以通过这个模板来创建容器服务 tomcat镜像--》run--》tomcat1容器 提供的服务器
可以通过这个镜像可以创建多个容器 最终服务器运行或者项目运行就是在容器中的

#### 容器 (container)
Docker利用容器技术 独立运行一个或者一个组应用 通过镜像来创建
启动 停止 删除 基本命令

目前就可以把这个容器理解为 一个建议的linux系统

#### 仓库：(repository)
存放镜像的地方 分为 公有 私有的

DockerHub 

都有容器服务 国内 配置镜像加速

安装Docker ->Typora

```
环境安装
```

1. 需要会一点点的linux的基础
2. CentOs7
3. 我们使用xshell连接 centos

```
# 系统内核时3.10.0以上的
[root@localhost /]# uname -r
3.10.0-1127.19.1.el7.x86_64
[root@localhost /]# 

```

系统的版本

```
[root@localhost /]# cat /etc/os-release
NAME="CentOS Linux"
VERSION="7 (Core)"
ID="centos"
ID_LIKE="rhel fedora"
VERSION_ID="7"
PRETTY_NAME="CentOS Linux 7 (Core)"
ANSI_COLOR="0;31"
CPE_NAME="cpe:/o:centos:centos:7"
HOME_URL="https://www.centos.org/"
BUG_REPORT_URL="https://bugs.centos.org/"

CENTOS_MANTISBT_PROJECT="CentOS-7"
CENTOS_MANTISBT_PROJECT_VERSION="7"
REDHAT_SUPPORT_PRODUCT="centos"
REDHAT_SUPPORT_PRODUCT_VERSION="7"

[root@localhost /]# 

```

安装

帮助文档

卸载旧的版本

```
$ sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

安装 需要的安装包

```
$ sudo yum install -y yum-utils
```

设置镜像的仓库

```
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo #默认是国外是十分慢
    
#换成阿里云的镜像
    
yum-config-manager \
    --add-repo \
    http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

更新yum索引

```
yum makecache fast
```



安装最新版的 Docker 引擎 docker -ce 社区版  ee企业版

```
yum install docker-ce docker-ce-cli containerd.io
```

启动docker

```
systemctl start docker
```

判断是否安装成功

```
[root@localhost /]# dokcer version
-bash: dokcer: 未找到命令
[root@localhost /]# docker version
Client: Docker Engine - Community
 Version:           19.03.13
 API version:       1.40
 Go version:        go1.13.15
 Git commit:        4484c46d9d
 Built:             Wed Sep 16 17:03:45 2020
 OS/Arch:           linux/amd64
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          19.03.13
  API version:      1.40 (minimum version 1.12)
  Go version:       go1.13.15
  Git commit:       4484c46d9d
  Built:            Wed Sep 16 17:02:21 2020
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.3.7
  GitCommit:        8fba4e9a7d01810a393d5d25a3621dc101981175
 runc:
  Version:          1.0.0-rc10
  GitCommit:        dc9208a3303feef5b3839f4323d9beb36df0a9dd
 docker-init:
  Version:          0.18.0
  GitCommit:        fec3683
[root@localhost /]# 

```

测试HelloWorld

```
docker run hello-world

[root@localhost /]# docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
0e03bdcc26d7: Pull complete 
Digest: sha256:4cf9c47f86df71d48364001ede3a4fcd85ae80ce02ebad74156906caff5378bc
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/

[root@localhost /]# 


```

查看下载Hellowrold镜像

```
docker images
```

卸载Docker

```
# 卸载依赖
$ sudo yum remove docker-ce docker-ce-cli containerd.io

# 删除目录
$ sudo rm -rf /var/lib/docker

# /var/lib/docker docker 默认工作目录
```



#### 阿里云镜像加速

1.登录案例云找到云镜像加速服务

2.加速地址

3.配置使用 我这里使用的是别人企业的

```
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://qiyb9988.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

![image-20200928190307445](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200928190307445.png)



```
# 修改成这个样子
vi /etc/docker/daemon.json
{
  "registry-mirrors": [
    "https://registry.docker-cn.com",
    "https://dockerhub.azk8s.cn",
    "https://reg-mirror.qiniu.com"
   ]
}

```



https://processon.com 画图软件

#### 回顾helloworld流程

![image-20200928192037784](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200928192037784.png)



#### 底层原理

Docker怎么工作的

Docker 是 client 和 server结构的系统、Docker的守护进程运行在主机上，通过sokcer从客户端访问

Dockerserver接受到Docker-client的指令 就会执行这个命令

![image-20200928192550931](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200928192550931.png)

  

Docker为什么比VM快?

1.Docker有比虚拟机更少的抽象层

2.Docker利用了是宿主机的内核，vm需要时GuestOS

![image-20200928192657778](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200928192657778.png)

所以说，新建一个容器的时候，dokcer不需要虚拟机一样重新加载一个操作系统，减少引导，虚拟机是加载CuestOS,分钟级别的，而docker是利用宿主机的操作系统这是一个非常快的

![image-20200928193010625](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200928193010625.png)

学习完毕所有的命令 回过头来这段理论，就会很清晰



#### Docker的常用的命令