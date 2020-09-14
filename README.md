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
'''java
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

'''


停止容器

docker pause myjava

docker unpause myjava

docker stop myjava

docker start -i myjava

'''
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
'''





