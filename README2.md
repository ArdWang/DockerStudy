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

#### 帮助命令

```
docker version # 显示docker版本信息
docker info    # 显示docker系统信息，包扣
docker 命令 --help # 帮助命令

```

帮助文档地址 https://docs.docker.com/reference/



#### 镜像命令

##### docker images

docker images --help

```
[root@localhost ~]# docker images --help

Usage:	docker images [OPTIONS] [REPOSITORY[:TAG]]

List images

Options:
  -a, --all             Show all images (default hides intermediate images)
      --digests         Show digests
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print images using a Go template
      --no-trunc        Don't truncate output
  -q, --quiet           Only show numeric IDs
[root@localhost ~]# 

[root@localhost ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
haproxy             latest              8e202ffaa1a8        2 weeks ago         93.3MB
pxc                 latest              7eab3380a35c        3 months ago        603MB
hello-world         latest              bf756fb1ae65        9 months ago        13.3kB
[root@localhost ~]# 

# 解析

RPOSITORY 镜像的仓库源
TAG       镜像的标签
IMAGE ID  镜像ID
CREATE    镜像的创建时间
SIZE      镜像的大小

# 可选项
  -a, --all             Show all images (default hides intermediate images) #练出所有的镜像
      --digests         Show digests
  -f, --filter filter   Filter output based on conditions provided
      --format string   Pretty-print images using a Go template
      --no-trunc        Don't truncate output
  -q, --quiet           Only show numeric IDs  # 只显示镜像ID
  
  # 常用命令
  docker images -a
  docker images -q
  
```

##### docker search 搜索镜像

```
docker search mysql

[root@localhost ~]# docker search mysql
NAME                              DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
mysql                             MySQL is a widely used, open-source relation…   9998                [OK]                
mariadb                           MariaDB is a community-developed fork of MyS…   3662                [OK]                
mysql/mysql-server                Optimized MySQL Server Docker images. Create…   731                                     [OK]
percona                           Percona Server is a fork of the MySQL relati…   512                 [OK]                
centos/mysql-57-centos7           MySQL 5.7 SQL database server                   83                                      
mysql/mysql-cluster               Experimental MySQL Cluster Docker images. Cr…   76                                      
centurylink/mysql                 Image containing mysql. Optimized to be link…   61                                      [OK]
bitnami/mysql                     Bitnami MySQL Docker Image                      45                                      [OK]
deitch/mysql-backup               REPLACED! Please use http://hub.docker.com/r…   41                                      [OK]
tutum/mysql                       Base docker image to run a MySQL database se…   35                                      
prom/mysqld-exporter                                                              31                                      [OK]
schickling/mysql-backup-s3        Backup MySQL to S3 (supports periodic backup…   30                                      [OK]
databack/mysql-backup             Back up mysql databases to... anywhere!         30                                      
linuxserver/mysql                 A Mysql container, brought to you by LinuxSe…   26                                      
centos/mysql-56-centos7           MySQL 5.6 SQL database server                   20                                      
circleci/mysql                    MySQL is a widely used, open-source relation…   19                                      
mysql/mysql-router                MySQL Router provides transparent routing be…   16                                      
arey/mysql-client                 Run a MySQL client from a docker container      15                                      [OK]
fradelg/mysql-cron-backup         MySQL/MariaDB database backup using cron tas…   8                                       [OK]
openshift/mysql-55-centos7        DEPRECATED: A Centos7 based MySQL v5.5 image…   6                                       
devilbox/mysql                    Retagged MySQL, MariaDB and PerconaDB offici…   3                                       
ansibleplaybookbundle/mysql-apb   An APB which deploys RHSCL MySQL                2                                       [OK]
widdpim/mysql-client              Dockerized MySQL Client (5.7) including Curl…   1                                       [OK]
jelastic/mysql                    An image of the MySQL database server mainta…   1                                       
monasca/mysql-init                A minimal decoupled init container for mysql    0                                       
[root@localhost ~]# 

# 可选项 通过收藏来过滤
-- filter-STARS=3000 #搜索出来的镜像 STARTS大于3000的
[root@localhost ~]# docker search mysql --filter=STARS=3000
NAME                DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
mysql               MySQL is a widely used, open-source relation…   9998                [OK]                
mariadb             MariaDB is a community-developed fork of MyS…   3662                [OK]                
[root@localhost ~]# 

```

##### docker pull

下载镜像

docker pull mysql

```
[root@localhost ~]# docker pull --help

Usage:	docker pull [OPTIONS] NAME[:TAG|@DIGEST]

Pull an image or a repository from a registry

Options:
  -a, --all-tags                Download all tagged images in the repository
      --disable-content-trust   Skip image verification (default true)
      --platform string         Set platform if server is multi-platform capable
  -q, --quiet                   Suppress verbose output


#如果不写版本 默认拉取得是 latest
[root@localhost ~]# docker pull mysql
Using default tag: latest
latest: Pulling from library/mysql
d121f8d1c412: Already exists 
f3cebc0b4691: Pull complete # 分层下载 docker images核心 联合文件系统
1862755a0b37: Pull complete 
489b44f3dbb4: Pull complete 
690874f836db: Pull complete 
baa8be383ffb: Pull complete 
55356608b4ac: Pull complete 
dd35ceccb6eb: Pull complete 
429b35712b19: Pull complete 
162d8291095c: Pull complete 
5e500ef7181b: Pull complete 
af7528e958b6: Pull complete 
Digest: sha256:e1bfe11693ed2052cb3b4e5fa356c65381129e87e38551c6cd6ec532ebe0e808 # 签名信息
Status: Downloaded newer image for mysql:latest
docker.io/library/mysql:latest  #真实地址
[root@localhost ~]# 

# 这个两个命令是相等得
docker pull mysql
docker pull docker.io/library/mysql:latest

# 指定版本下载
[root@localhost ~]# docker pull mysql:5.7
5.7: Pulling from library/mysql
d121f8d1c412: Already exists  #存在联合文件系统 有了就不需要去下载
f3cebc0b4691: Already exists 
1862755a0b37: Already exists 
489b44f3dbb4: Already exists 
690874f836db: Already exists 
baa8be383ffb: Already exists 
55356608b4ac: Already exists 
277d8f888368: Pull complete 
21f2da6feb67: Pull complete 
2c98f818bcb9: Pull complete 
031b0a770162: Pull complete 
Digest: sha256:14fd47ec8724954b63d1a236d2299b8da25c9bbb8eacc739bb88038d82da4919
Status: Downloaded newer image for mysql:5.7
docker.io/library/mysql:5.7
[root@localhost ~]# 

[root@localhost ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
mysql               5.7                 ef08065b0a30        2 weeks ago         448MB
mysql               latest              e1d7dc9731da        2 weeks ago         544MB
haproxy             latest              8e202ffaa1a8        2 weeks ago         93.3MB
pxc                 latest              7eab3380a35c        3 months ago        603MB
hello-world         latest              bf756fb1ae65        9 months ago        13.3kB
[root@localhost ~]# 

```

##### docker rmi 删除镜像

```
[root@localhost ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
mysql               5.7                 ef08065b0a30        2 weeks ago         448MB
mysql               latest              e1d7dc9731da        2 weeks ago         544MB
haproxy             latest              8e202ffaa1a8        2 weeks ago         93.3MB
pxc                 latest              7eab3380a35c        3 months ago        603MB
hello-world         latest              bf756fb1ae65        9 months ago        13.3kB

# 通过id删除 通过指定得容易
[root@localhost ~]# docker rmi ef08065b0a30
Untagged: mysql:5.7
Untagged: mysql@sha256:14fd47ec8724954b63d1a236d2299b8da25c9bbb8eacc739bb88038d82da4919
Deleted: sha256:ef08065b0a302111b56966aa92c89fa0bacdfc537741cbca88a15b10f14332ca
Deleted: sha256:c8c81ac92392c394197759ca3d50f5f843d85ac1550d8c0bb2b21adc7334100d
Deleted: sha256:2dc86a1b9b92e7c946c684bd349e448d7c4fbb3236686e1a48ddfe5adb86a425
Deleted: sha256:97b541df82456d38e987b630870fcd4e39f05f016717652466b3466841f4162e
Deleted: sha256:aded9a11fc54761c770a9075cfc2d0bb72c72b59171a56cfa4322ab2b2d416e7
[root@localhost ~]# 

# 递归删除
[root@localhost ~]# docker rmi -f $(docker images -aq)

先删除容器，再删除镜像

删除所有已停止的镜像 docker rm $(docker ps -a -q)
删除所有镜像 docker rmi $(docker images -q)
强制删除

强制删除所有镜像 docker rmi -f $(docker images -q)

```



#### 容器命令

说明：我们有了镜像才可以创建容器 linux 下载一个centos镜像来测试学习

```
docker pull centos
```

##### 新建容器并启动

```
docker run --help
docker run [可选参数] image

# 参数说明
--name="Name" 容器名字 tomcat01 tomcat02 用来区分容器
-d 后台方式运行 ja nohup
-it 交互方式运行 进入容易查看内容 
-p 指定容器得端口 -p 8080:8080 
				-p主机端口 容器端口 （常用）
-P 随机指定端口

# 测试 启动并进入容器
[root@localhost ~]# docker run -it centos /bin/bash
[root@7a7dfcac3efe /]# 

[root@7a7dfcac3efe /]# ls # 查看容器内得 Centos 基础版本 很多命令不完善得
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var

退出 exit
从容器中退出主机
[root@7a7dfcac3efe /]# exit
exit
[root@localhost ~]# ls

```

##### 列出所有得运行容器

```
# docker ps 命令
-a #列出正在运行得容器+带有运行得历史运行过容器
n=? # 显示最近创建得容器
-q # 只显示容器得编号


[root@localhost /]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[root@localhost /]# 

# 查看曾经运行过得容器
[root@localhost /]# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                          PORTS               NAMES
7a7dfcac3efe        centos              "/bin/bash"         3 minutes ago       Exited (0) About a minute ago                       naughty_solomon
[root@localhost /]# 

```

##### 退出容器

```
exit #直接停止并退出
ctrl+p+q 不停止退出

[root@localhost /]# docker run -it centos /bin/bash
[root@6f0336c943bb /]# [root@localhost /]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
6f0336c943bb        centos              "/bin/bash"         17 seconds ago      Up 16 seconds                           mystifying_saha
[root@localhost /]# 

```



##### 删除容器

```
docker rm 容器id  #删除指定得容器 不能删除正在运行得容器 如果要强制 删除 rm -f
docker rm -f $(docker ps -aq) # 删除所有得容器

docker ps -a -q|xargs  qocker rm # 也可以删除所有得容器
```

##### 启动和停止容器得操作

```
docker start 容器id
docker restart 容器id
docker stop 容器id 
docker kill 容器id #强制删掉
```

##### 常用其它得命令

后台启动容器

```
# 命令 docker run -d 镜像名
[root@localhost ~]# docker run -d centos
# 问题 docker ps, 发现centos停止了

# 常见的坑 docker 容器使用后台运行，就必须要有一个前台的进程，docker发现没有应用，就会自己动停止
# nginx 容器启动后，发现自己没有提供服务，就会立刻停止，就是没有程序了

```

##### 查看日志命令

```
docker logs --help

docker logs -tf --tail 容器 没有日志

退出日志 ctrl+c

"while true;do echo kuangshen; sleep 1;done"


[root@localhost ~]# docker run -d centos /bin/sh -c "while true; do echo kuangshen;sleep 1;done"

[root@localhost ~]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
615ecbb685f6        centos              "/bin/sh -c 'while t…"   4 seconds ago       Up 3 seconds                            wizardly_easley

[root@localhost ~]# docker logs --help

Usage:	docker logs [OPTIONS] CONTAINER

Fetch the logs of a container

Options:
      --details        Show extra details provided to logs
  -f, --follow         Follow log output
      --since string   Show logs since timestamp (e.g. 2013-01-02T13:23:37) or relative (e.g. 42m for 42 minutes)
      --tail string    Number of lines to show from the end of the logs (default "all")
  -t, --timestamps     Show timestamps
      --until string   Show logs before a timestamp (e.g. 2013-01-02T13:23:37) or relative (e.g. 42m for 42 minutes)

# 显示10条日志
[root@localhost ~]# docker logs -tf --tail 10 615ecbb685f6

# 显示全部的日志
[root@localhost ~]# docker logs -tf 615ecbb685f6



```

##### 查看容器中进程信息

```
top 命令 
容器id
docker top 615ecbb685f6

[root@localhost ~]# docker top --help

Usage:	docker top CONTAINER [ps OPTIONS]

Display the running processes of a container
[root@localhost ~]# docker top 615ecbb685f6
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                4188                4171                0                   18:19               ?                   00:00:00            /bin/sh -c while true; do echo kuangshen;sleep 1;done
root                4587                4188                0                   18:24               ?                   00:00:00            /usr/bin/coreutils --coreutils-prog-shebang=sleep /usr/bin/sleep 1
[root@localhost ~]# 

```



##### 查看镜像的元素据

```
# 命令 docker inspect

[root@localhost ~]# docker inspect --help

Usage:	docker inspect [OPTIONS] NAME|ID [NAME|ID...]

Return low-level information on Docker objects

Options:
  -f, --format string   Format the output using the given Go template
  -s, --size            Display total file sizes if the type is container
      --type string     Return JSON for specified type
[root@localhost ~]# 

# 命令 


[root@localhost ~]# docker inspect 615ecbb685f6
[
    {
        "Id": "615ecbb685f653582cec7e734c71218774b2b75d095128db4f42105b89953181",
        "Created": "2020-09-30T10:19:38.741631719Z",
        "Path": "/bin/sh",
        "Args": [
            "-c",
            "while true; do echo kuangshen;sleep 1;done"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 4188,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2020-09-30T10:19:38.977843915Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:0d120b6ccaa8c5e149176798b3501d4dd1885f961922497cd0abef155c869566",
        "ResolvConfPath": "/var/lib/docker/containers/615ecbb685f653582cec7e734c71218774b2b75d095128db4f42105b89953181/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/615ecbb685f653582cec7e734c71218774b2b75d095128db4f42105b89953181/hostname",
        "HostsPath": "/var/lib/docker/containers/615ecbb685f653582cec7e734c71218774b2b75d095128db4f42105b89953181/hosts",
        "LogPath": "/var/lib/docker/containers/615ecbb685f653582cec7e734c71218774b2b75d095128db4f42105b89953181/615ecbb685f653582cec7e734c71218774b2b75d095128db4f42105b89953181-json.log",
        "Name": "/wizardly_easley",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "Capabilities": null,
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "KernelMemory": 0,
            "KernelMemoryTCP": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": false,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/f9fb89040de94c4dc537ea80f5fa38ae0a0f8fd5732893d3e87c23020ab8b9f7-init/diff:/var/lib/docker/overlay2/2618e3fe75e57cc2633cdbc57add7b3bb5ba74efae7dd0fde62e97690d2ed39d/diff",
                "MergedDir": "/var/lib/docker/overlay2/f9fb89040de94c4dc537ea80f5fa38ae0a0f8fd5732893d3e87c23020ab8b9f7/merged",
                "UpperDir": "/var/lib/docker/overlay2/f9fb89040de94c4dc537ea80f5fa38ae0a0f8fd5732893d3e87c23020ab8b9f7/diff",
                "WorkDir": "/var/lib/docker/overlay2/f9fb89040de94c4dc537ea80f5fa38ae0a0f8fd5732893d3e87c23020ab8b9f7/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "615ecbb685f6",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "while true; do echo kuangshen;sleep 1;done"
            ],
            "Image": "centos",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {
                "org.label-schema.build-date": "20200809",
                "org.label-schema.license": "GPLv2",
                "org.label-schema.name": "CentOS Base Image",
                "org.label-schema.schema-version": "1.0",
                "org.label-schema.vendor": "CentOS"
            }
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "56db8db008c0225fa35508ff3f72eb362bc8c51cc9f3f9d5f0571510b07dc83b",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {},
            "SandboxKey": "/var/run/docker/netns/56db8db008c0",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "3b18c9d8d07dbfe7099eca126c0a17cc023c9547ef6a7fc6b8dd78007c28013e",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "3c904616988c63c272b88f779efa6f30aa06214e4fc5ed94d48b1aefa5ec1b3e",
                    "EndpointID": "3b18c9d8d07dbfe7099eca126c0a17cc023c9547ef6a7fc6b8dd78007c28013e",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null
                }
            }
        }
    }
]
[root@localhost ~]# 

```

##### 进入当前正在运行的容器

```
通常容器使用后台运行 需要进入容器 修改一些配置
# docker
docker exec -it 容器id bashshell

[root@localhost ~]# docker exec -it 615ecbb685f6 /bin/bash
[root@615ecbb685f6 /]# ls
bin  dev  etc  home  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
[root@615ecbb685f6 /]#

# 测试
[root@615ecbb685f6 /]# ps -ef
UID         PID   PPID  C STIME TTY          TIME CMD
root          1      0  0 03:40 ?        00:00:11 /bin/sh -c while true; do echo kuangshen;sleep 1;done
root      24394      0  0 10:28 pts/0    00:00:00 /bin/bash
root      24437      1  0 10:29 ?        00:00:00 /usr/bin/coreutils --coreutils-prog-shebang=sleep /usr/bin/sleep 1
root      24438  24394  0 10:29 pts/0    00:00:00 ps -ef
[root@615ecbb685f6 /]# 

# 方式2
docker attach 容器id
测试
# docker exec 进入容器后开启一个新的终端,可以在里面操作(常用)
# docker attach 进入容器正在执行的终端 不会启动新的进程

```

##### 从容器内拷贝文件到主机上

```
docker cp 容器id内路径 目的的主机路径

# 进入docker容器内部
[root@localhost home]# docker attach b36fbea55c53
# 在容器内部新建一个文件
[root@b36fbea55c53 /]# cd /home
[root@b36fbea55c53 home]# ls
[root@b36fbea55c53 home]# touch test.java
[root@b36fbea55c53 home]# ls
test.java
[root@b36fbea55c53 home]# exit  
exit
[root@localhost home]# docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[root@localhost home]# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                     PORTS               NAMES
b36fbea55c53        centos              "/bin/bash"         2 minutes ago       Exited (0) 9 seconds ago                       sad_curran

# 将这个文件拷贝出来到主机上
[root@localhost home]# docker cp b36fbea55c53:/home/test.java /home
[root@localhost home]# ls
java.tar.gz  kuangshen.java  newproject  project  soft  test.java  xiaowang
[root@localhost home]# 

docker data
# 拷贝是一个手动过程 为了使用-v 数据卷的技术 可以实现自动同步
```

学习方式: 将所有命令敲一遍 自己记录笔记

##### 小结

![image-20201003191738994](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201003191738994.png)

![image-20201003191953690](C:\Users\Administrator\Desktop\image-20201003191953690.png)

![image-20201003192101954](C:\Users\Administrator\Desktop\image-20201003192101954.png)

![image-20201003192117673](C:\Users\Administrator\Desktop\image-20201003192117673.png)

```
attach # 当前shell下的 attach连接到指定运行镜像
build  # 通过dockerfile定制镜像
commit # 提交当前容器为新的镜像
cp  # 从容器中拷贝指定文件或者目录到宿主机中
create  #创建一个新的容器，同run 但不启动容器
diff # 查看docker容器变化
events # 从docker服务获取容器实时事件
exec # 在存在的容器上运行命令
export #导出容器的内容作为一个tar归档文件 [对应import]
history  #展示一个镜像形成历史
images # 列出系统当前的镜像
import # 从tar包中的内容创建一个新的文件系统映像[对应export]
info # 显示系统相关信息
inspect # 查看容器详细信息
kill # kill指定docker容器
load # 从一个tar包中加载一个镜像[对应save]
login # 注册或者登录一个docker源服务器
logout # 从当前Docker registry 退出
logs 输出当前容器的日志
port # 查看映射端口对应的容器内部源端口
pause # 暂停容器
ps # 列出容器列表
pull # 从docker镜像源服务器拉取指定的镜像或者库镜像
push # 推送指定镜像或者镜像至docker源服务器
restart # 重启运行的容器
rm # 移除一个或者多个容器
rmi # 移除一个或者多个镜像[无容器使用该镜像可以删除,否则需要删除相关容器才可以继续或 -f 强制删除]
run # 创建一个新的容器并运行一个命令
save # 保存一个镜像为一个tar包[对应 load]
search # 在docker hub中搜索镜像
start # 容器容器
stop # 停止容器
tag # 给源中镜像打标签
top # 查看容器中运行的进程信息
unpause # 取消暂停容器
version # 查看docker版本号
wait # 截取容器停止时的退出状态值


```

docker的命令是非常的多的。上面我们学习的哪些都是些常用的命令

```
接下来我们一起练习
```

##### 作业练习

```
第一个作业
Docker 安装 Nginx

docker search nginx

docker pull nginx

```

```
1.搜索镜像  search 可以帮助文档信息
2.下载镜像
3.运行测试

[root@localhost ~]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
nginx               latest              7e4d58f0e5f3        3 weeks ago         133MB
haproxy             latest              8e202ffaa1a8        3 weeks ago         93.3MB
centos              latest              0d120b6ccaa8        7 weeks ago         215MB
# 运行nginx 进行测试 -d 后台运行 --name 起一个名字 
# -p 宿主机端口 容器内部端口
[root@localhost ~]# docker run -d --name nginx01 -p 3344:80 nginx 
81fd854adc4553d826d70c91e25b11944f89346411e8df0030eb72f98b648238
[root@localhost ~]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
81fd854adc45        nginx               "/docker-entrypoint.…"   10 seconds ago      Up 7 seconds        0.0.0.0:3344->80/tcp   nginx01
# 测试
[root@localhost ~]# curl localhost:3344
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
[root@localhost ~]# 

# 进入容器
[root@localhost ~]# docker exec -it nginx01 /bin/bash
root@81fd854adc45:/# whereis nginx
nginx: /usr/sbin/nginx /usr/lib/nginx /etc/nginx /usr/share/nginx
root@81fd854adc45:/# cd /etc/nginx
root@81fd854adc45:/etc/nginx# ls
conf.d	fastcgi_params	koi-utf  koi-win  mime.types  modules  nginx.conf  scgi_params	uwsgi_params  win-utf
root@81fd854adc45:/etc/nginx# 

# 停止容器
[root@localhost ~]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
81fd854adc45        nginx               "/docker-entrypoint.…"   8 minutes ago       Up 8 minutes        0.0.0.0:3344->80/tcp   nginx01
[root@localhost ~]# docker stop
"docker stop" requires at least 1 argument.
See 'docker stop --help'.

Usage:  docker stop [OPTIONS] CONTAINER [CONTAINER...]

Stop one or more running containers
[root@localhost ~]# docker stop 81fd854adc45
81fd854adc45
[root@localhost ~]#

```



##### 端口暴露的慨念

![image-20201004132616072](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201004132616072.png)



思考问题:我们每次改动 nginx配置文件，都需要进入容器内部?十分麻烦，我要是可以在容器外部提供一个映射路径，达到在容器修改文件名，容器就可以自动修改? -v 数据卷的方式

```
作业:docker 安装 tomcat

# 官方的使用 $ docker run -it --rm tomcat:9.0
# 我们之前的启动都是后台，停止容器之后，容器还是可以查到 一般来测试 用完就自动删除

# 先下载再启动
docker pull tomcat

# 启动运行
[root@localhost ~]# docker run -d -p 3355:8080 --name tomcat01 tomcat

# 进入容器
root@989d275bf22c:/usr/local/tomcat# ls
BUILDING.txt	 LICENSE  README.md	 RUNNING.txt  conf  logs	    temp     webapps.dist
CONTRIBUTING.md  NOTICE   RELEASE-NOTES  bin	      lib   native-jni-lib  webapps  work
root@989d275bf22c:/usr/local/tomcat# ls -al

# 发现问题 liunx 命令少了 没有webapps 阿里云原因 还有镜像原因 默认是最少的镜像 把不必要的都删除掉了
# 保证可以最少的

# 处理方法如下
root@989d275bf22c:/usr/local/tomcat/webapps.dist# cd ..
root@989d275bf22c:/usr/local/tomcat# cp -r webapps.dist/* webapps

```

外网访问是可以的

思考问题： 我们以后要部署项目，如果每次都要进入容器十分麻烦，我要是可以在容器外部提供一个映射路径，达到在容器修改文件名，容器就可以自动修改? -v 数据卷的方式

我们在外部放入项目 就自动同步到内部就好了

docker 容器 tomact -网站 docker mysql



```
作业3 部署 es kibana

elasticsearch

# es 暴露的端口很多
# es 耗内存
# es
# 网络配置

# 启动 elasticsearch
$ docker run -d --name elasticsearch02 -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" elasticsearch:7.6.2

# 启动了服务器 Linux 就很卡  docker status 查看 cpu状态
# es启动特别耗内存 1 xg 1核2g
# 停止整个docker
# 查看 docker stats
# 测试 es是否成功了
# 赶紧关闭，增加内存的限制

[root@localhost ~]# curl localhost:9200

{
  "name" : "73d9d8563afc",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "9hYVluICTqKFDb0ZycJ7Cg",
  "version" : {
    "number" : "7.6.2",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "ef48eb35cf30adf4db14086e8aabd07ef6fb113f",
    "build_date" : "2020-03-26T06:34:37.794943Z",
    "build_snapshot" : false,
    "lucene_version" : "8.4.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}

# 可以通过修改配置文件来增加使用内存的限制 -e 环境配置修改
# 通过以下就可以更改

docker run -d --name elasticsearch02 -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" -e ES_JAVA_OPTS="-Xms64m -Xmx512m" elasticsearch:7.6.2

[root@localhost ~]# curl localhost:9200
{
  "name" : "7127d67c8ab9",
  "cluster_name" : "docker-cluster",
  "cluster_uuid" : "GgyCknP9SviAQIRv2V2SjA",
  "version" : {
    "number" : "7.6.2",
    "build_flavor" : "default",
    "build_type" : "docker",
    "build_hash" : "ef48eb35cf30adf4db14086e8aabd07ef6fb113f",
    "build_date" : "2020-03-26T06:34:37.794943Z",
    "build_snapshot" : false,
    "lucene_version" : "8.4.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
[root@localhost ~]# 


```

作业：使用 kibana 内部端口  es 如何才能连接过去

![image-20201005194011198](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201005194011198.png)



解决一些网络问题：https://www.cnblogs.com/python-wen/p/11224828.html

*WARNING: IPv4 forwarding is disabled. Networking will not work.*



#### 可视化

Portainer 可视化面板

Docker 图形化管理工具 后台面板进行操作



```java
# portainer 安装
    
docker run -d -p 8088:9000 -v /var/run/docker.sock:/var/run/docker.sock --restart=always --privileged=true portainer/portainer
    
docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock --restart=always --name prtainer --privileged=true portainer/portainer
```

访问测试

http://192.168.3.47:9000

通过它来访问了:



![image-20201006084854607](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201006084854607.png)



选择本地的

![image-20201006084912688](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201006084912688.png)



然后是用一个这样子的面板

![image-20201006085017889](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201006085017889.png)



可视化面板

![image-20201006085419591](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201006085419591.png)



我们平时不会用 测试一下即可



Rancher (CI/CD再用)



#### Docker镜像的讲解

##### 镜像是什么

镜像是一种轻量级可执行的独立软件包, 用来打包软件运行环境和基于运行环境开发的软件，它包含运行软件所需要的所有内容，包扣代码，运行时，库。环境变量和配置文件。

所有的应用直接打包部署 就可以直接跑起来

1.从远程仓库下载

2.从别人哪里拷贝

3.自己做一个



#### Docker镜像的加载原理

```
UnionFS(联合文件系统)   
```

一层一层的叠加

共用文件



docker镜像加载原理

![image-20201006090057454](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201006090057454.png)

虚拟机是分钟级别

容器是秒级的



##### 理解

![image-20201007190506164](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201007190506164.png)

![image-20201007190650064](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201007190650064.png)

![image-20201007190748577](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201007190748577.png)

![image-20201007191100184](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201007191100184.png)

```java
特点
```

Dokcer 镜像都是只读的，当容器启动时，一个新的可写层被加载到镜像的顶部!

这一层就是我们通常说的容器层，容器之下的都叫镜像层

pull 远程下载下来了

![image-20201007191756770](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201007191756770.png)



如何提交一个自己镜像

#### Commit镜像

```java
docker commit 提交容器成为一个新的副本

 #命令和git相似
docker commit -m="提交的描述信息" -a-="作者" 容器id 目标镜像名:[TAG]
```

```
# 启动一个默认的 tomcat

# 发现这个默认的tomcat是没有webapps的一个应用的，镜像的原因，官方的镜像

# 自己拷贝了一份基本的文件

# 将操作过的容器 通过commit提交一个新的镜像 我们以后就使用我们修改过的镜像，这就是我们修改过的镜像

[root@localhost ~]# docker ps
CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS              PORTS                                            NAMES
e69f74b3f8ff        tomcat                "catalina.sh run"        9 minutes ago       Up 9 minutes        0.0.0.0:8080->8080/tcp                           quizzical_stonebraker
956a33482450        portainer/portainer   "/portainer"             2 days ago          Up 2 days           0.0.0.0:9000->9000/tcp                           hopeful_mccarthy
7127d67c8ab9        elasticsearch:7.6.2   "/usr/local/bin/dock…"   2 days ago          Up 2 days           0.0.0.0:9200->9200/tcp, 0.0.0.0:9300->9300/tcp   elasticsearch02
[root@localhost ~]# docker commit -a="superbread" -m="add webapps app" e69f74b3f8ff tomcat02:1.0
sha256:f644b9fa75d3c289b05b1b520c11bad075a38c08be820198fbd914bb04c754e2
[root@localhost ~]# docker images
REPOSITORY            TAG                 IMAGE ID            CREATED             SIZE
tomcat02              1.0                 f644b9fa75d3        7 seconds ago       652MB
tomcat                9.0                 f796d3d2c195        3 weeks ago         647MB
tomcat                latest              f796d3d2c195        3 weeks ago         647MB
redis                 latest              84c5f6e03bf0        3 weeks ago         104MB
nginx                 latest              7e4d58f0e5f3        3 weeks ago         133MB
haproxy               latest              8e202ffaa1a8        4 weeks ago         93.3MB
centos                latest              0d120b6ccaa8        8 weeks ago         215MB
portainer/portainer   latest              62771b0b9b09        2 months ago        79.1MB
elasticsearch         7.6.2               f29a1ee41030        6 months ago        791MB
[root@localhost ~]# 


```



学习方式 说明 先理解概念 但一定实践 理论实践操作

```
如果你想要保存容器的状态，就可以通过commit来提交 获得一个镜像
就好比我们以前学习虚拟机的时候 快照
```

到了这里才算是入门 Docker 认真吸收练习，该休息



#### 容器数据卷

##### 什么是容器数据卷

docker的理念回顾

将应用和环境打包成一个镜像!

数据?如果数据在容器中，那么我们容器删除，数据就会失去 需求 数据可以持久化

Mysql 容器删了 删库跑路 需求 mysql数据可以存储在本地

容器之间可以有一个共享的技术！

Docker容器中产生的数据可以同步到本地 Docker容器产生的数据，同步到本地

这就是卷技术 目录挂载 将我们的容器内的目录 挂在Linux上面!



![image-20201009183613283](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201009183613283.png)



总结一句话 容器的持久化的同步操作 容器可以数据共享的

##### 使用数据卷

```java
方式一；直接使用 -v
[root@localhost ~]# docker run -it -v
docker run -it -v 主机目录地址 容器内部目录 -p 端口做映射

[root@localhost ~]# cd /home
[root@localhost home]# ls
java.tar.gz  kuangshen.java  newproject  project  soft  test.java  xiaowang
[root@localhost home]# docker run -it -v /home/ceshi:/home centos /bin/bash

# 启动起来的时候我们可以通过 docker inspect 容器id
```

挂载

![image-20201009184813285](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201009184813285.png)

测试文件同步的效果

![image-20201009185123821](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201009185123821.png)



再来测试

1.停止容器

2.宿主机上修改文件

3.启动容器

4.容器内依旧可以同步

![image-20201009185540614](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201009185540614.png)

好处：我们以后修改 只需要在本地修改即可，容器内部会自动同步!

#### DockerFile



#### Docker 网络



企业实战



Docker Compose



CI/CD jenkins 流水线！