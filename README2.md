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







解决一些网络问题：https://www.cnblogs.com/python-wen/p/11224828.html

*WARNING: IPv4 forwarding is disabled. Networking will not work.*



