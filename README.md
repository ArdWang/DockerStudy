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





