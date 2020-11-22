# DockerStudy
This is DockerStudy


查看虚拟机 Centos7 ip地址 ip address
查看 ens33 就行 192.168.3.47/24

cd 到项目种 执行 npm run dev 前端的项目进入 后端直接用 idea打开就可以了

安装失败 node-sass
更换 packeage.json 版本号
"sass-loader": "4.1.1",
 "node-sass": "4.13.1",

使用以下安装
Install from mirror in China
npm install -g mirror-config-china --registry=http://registry.npm.taobao.org
npm install node-sass

Swagger


touch 创建文档

echo 写入文件

cat hello.txt 查看

cd / 根目录

vi hello.txt 编辑

复制文件或者目录

cp hello.txt new.txt

复制文件夹
cp -r myproject newproject

cd .. 进入上一层指令

rm -r  myproject  删除文件 

rm -rf 删除

移动文件夹或文件
mv -f newproject /home

cd home

ls -l 查看文件的信息


文件属性

d-lbc 目录|链接|存储设备|串行设备

-rw-r--r-- 文件

属性权限
rwx- 读|写|执行|还没有权限|

修改权限的指令

chmod 700 hello.txt  数字怎么来的  读 是 4 写 是2  执行 是 1 累加是 4+2+1 = 7

ls -l hello.txt

创建新的用户
adduser xiaowang

passwd xiaowang

密码 wangjing123

防火墙

firewall-cmd --state

service firewall start
service firewall stop
service firewall restart

开放端口

firewall-cmd --permanent --add-port=8080-8085/tcp

firewall-cmd --reload

firewall-cmd --permanent --remove-port=8080-8085/tcp

上面规则怎么写 下面就怎么弄

查看防火墙端口

firewall-cmd --permanent --list-ports

防火墙加载
firewall-cmd --reload


firewall-cmd --permanent --list-services

显示 dhcpv6-client ssh


ks8

Docker 虚拟机 是轻量级别得虚拟机  vmall是重量级别得虚拟机

安装docker 首先运行 yum -y update

yum install -y docker

-y 代表yes选择

启动与关闭与重启

service docker start
service docker stop
service docker restart

在线安装镜像

设置加速器 http://get.daocloud.io/#install-docker

curl -sSL https://get.daocloud.io/docker | sh

java镜像

docker search java

docker pull java

使用 docker pull  docker.io/java

docker 安装镜像
docker images

save 保存镜像  docker save java > /home/java.tar.gz

导出镜像  docker load < /home/java.tar.gz

docker images

docker rmi java

启动容器

docker run -it --name java bash

映射端口 -p 真实宿主机子
docker run -it --name myjava -p 9000:8000 -p 9001:8085 java bash  

文件目录的映射 宿主机目录:
docker run -it --name myjava -v /home/project:/soft --privileged java bash 

cd /home 

mikdir project

ls

docker run -it -p 9000:8080 -p 9001:8085 -v /home/project:/soft --privileged --name myjava  docker.io/java bash

 进入之后
```java
root@0ebddd7a520a:/# 

bash: cd: /soft#: No such file or directory
root@0ebddd7a520a:/# cd /soft
root@0ebddd7a520a:/soft# ls
root@0ebddd7a520a:/soft# touch hello.txt
root@0ebddd7a520a:/soft# echo Thanks > hello.txt
root@0ebddd7a520a:/soft# exit
exit
[root@localhost home]# 

[root@localhost home]# ls
java.tar.gz  newproject  project  xiaowang
[root@localhost home]# cd project
[root@localhost project]# ls
hello.txt
[root@localhost project]# cat hello.txt
Thanks
[root@localhost project]# 

```


停止容器

docker pause myjava

docker unpause myjava

docker stop myjava

docker start -i myjava

```java
ARNING! The remote SSH server rejected X11 forwarding request.
Last login: Mon Sep 14 17:56:13 2020 from 192.168.3.37
[root@localhost ~]# docker pause myjava
myjava
[root@localhost ~]# docker unpause myjava
myjava
[root@localhost ~]# docker stop myjava
myjava
[root@localhost ~]# docker rm myjava
myjava
[root@localhost ~]# docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
[root@localhost ~]# 
```

mysql 集群方案

reolication 快

pxc 慢 性能高

建议PXC 使用 PerconaServer mysql改进版 性能提升很大

安装PXC镜像
第一种方式

```java

docker pull percona/percona-xtradb-cluster

```
第二种方式

```java
docker load < /home/soft/pxc.tar.gz

docker.io/percona/percona-xtradb-cluster

```

修改名字

```java

docker tag docker.io/percona/percona-xtradb-cluster pxc

docker rmi docker.io/percona/percona-xtradb-cluster
```

创建内部网络

```java
docker network create net1

docker network inspect net1

docker network rm net1

docker network create --subnet=172.18.0.0/24 net1

docker inspect net1

```

创建 Docker 卷
容器中得PXC节点映射数据目录得解决办法

```java
docker volume create --name v1

"/var/lib/docker/volumes/v1/_data",

docker rm v1

```

创建PXC容器 创建一个可以同步得去执行数据

```java
docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=abc123456 -e CLUSTER_NAME=PXC -e XTRABACKUP_PASSWORD=abc123456 -v v1:/var/lib/mysql --privileged --name=node1 --net=net1 --ip 172.18.0.2 pxc

docker run -d -p 3307:3306 -e MYSQL_ROOT_PASSWORD=abc123456 -e CLUSTER_NAME=PXC -e XTRABACKUP_PASSWORD=abc123456 -e CLUSTER_JOIN=node1 -v v2:/var/lib/mysql --privileged --name=node2 --net=net1 --ip 172.18.0.3 pxc 

docker run -d -p 3308:3306 -e MYSQL_ROOT_PASSWORD=abc123456 -e CLUSTER_NAME=PXC -e XTRABACKUP_PASSWORD=abc123456 -e CLUSTER_JOIN=node1 -v v3:/var/lib/mysql --privileged --name=node3 --net=net1 --ip 172.18.0.4 pxc

docker run -d -p 3309:3306 -e MYSQL_ROOT_PASSWORD=abc123456 -e CLUSTER_NAME=PXC -e XTRABACKUP_PASSWORD=abc123456 -e CLUSTER_JOIN=node1 -v v4:/var/lib/mysql --privileged --name=node4 --net=net1 --ip 172.18.0.5 pxc

docker run -d -p 3310:3306 -e MYSQL_ROOT_PASSWORD=abc123456 -e CLUSTER_NAME=PXC -e XTRABACKUP_PASSWORD=abc123456 -e CLUSTER_JOIN=node1 -v v5:/var/lib/mysql --privileged --name=node5 --net=net1 --ip 172.18.0.6 pxc

```

创建 Haproxy配置文件

```

touch /home/soft/haproxy.cfg

```
具体可以参考这个教程

https://zhangge.net/5125.html

创建命令


vi /home/soft/haproxy.cfg


```java

global
#工作目录
chroot /usr/local/etc/haproxy
#日志文件，使用rsyslog服务中local5日志设备（/var/log/local5），等级info
log 127.0.0.1 local5 info
#守护进程运行
daemon
defaults
log global
log global
mode http
#日志格式
option httplog
#日志中不记录负载均衡的心跳检测记录
option dontlognull
#连接超时（毫秒）
timeout connect 5000
#客户端超时（毫秒）
timeout client 50000
#服务器超时（毫秒）
timeout server 50000
#监控界面
listen admin_stats
#监控界面的访问的IP和端口
bind 0.0.0.0:8888
#访问协议
mode http
#URI相对地址
stats uri /dbs
#统计报告格式
stats realm Global\ statistics
#登陆帐户信息
stats auth admin:abc123456
#数据库负载均衡
listen proxy‐mysql
#访问的IP和端口
bind 0.0.0.0:3306
#网络协议
mode tcp
#负载均衡算法（轮询算法）
#轮询算法：roundrobin
#权重算法：static‐rr
#最少连接算法：leastconn
#请求源IP算法：source
balance roundrobin
#日志格式
option tcplog
#在MySQL中创建一个没有权限的haproxy用户，密码为空。Haproxy使用这个账户对MySQL数据库
心跳检测
option mysql‐check user haproxy
server MySQL_1 172.18.0.2:3306 check weight 1 maxconn 2000
server MySQL_2 172.18.0.3:3306 check weight 1 maxconn 2000
server MySQL_3 172.18.0.4:3306 check weight 1 maxconn 2000
server MySQL_4 172.18.0.5:3306 check weight 1 maxconn 2000
server MySQL_5 172.18.0.6:3306 check weight 1 maxconn 2000
#使用keepalive检测死链
option tcpka

```

创建第1个Haproxy负载均衡服务器

```java


docker run -it -d -p 4001:8888 -p 4002:3306 -v /home/soft/haproxy:/usr/local/etc/haproxy --name h1 --privileged --net=net1 --ip 172.18.0.7 haproxy





docker exec -it h1 bash

//进入
haproxy -f /usr/local/etc/haproxy/haproxy.cfg


```

在mysql种运行
 
CREATE USER 'haproxy'@'%' IDENTIFIED BY '';



更新到其它的连接 https://github.com/ArdWang/DockerStudy/blob/master/README2.md













