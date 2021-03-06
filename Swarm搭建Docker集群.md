## Swarm搭建Docker集群
Swarm是Docker官方提供的一个集群管理工具。

https://blog.csdn.net/chenxing109/article/details/84657582

### 环境准备
这里用两台机器来搭建,分别如下:

swarm01  192.168.100.61

swarm02  192.168.100.62

### 安装docker

1.编辑hosts文件
```bash
vim /etc/hosts
设置两台主机的对应关系
192.168.100.61 swarm01
192.168.100.62 swarm02
```
2.关闭防火墙

3.修改docker监听端口

4.重启docker服务

### Swarm安装和集群创建
1.swarm镜像下载
```bash
在两台机器上分别安装swarm
$ docker pull swarm
```
2.在61初始化swarm
```bash
$ docker swarm init --advertise-addr  192.168.100.61
```
3.添加集群节点
```bash
然后在swarm02机器上执行以下命令
$ docker swarm join --token SWMTKN-1-2wxaigf8ci95yhafoq43lw1nkn5e9ax7tsnn4bibofpz8h9yt2-8hw0144i6f9itsfnvksoc29d1 192.168.100.61:2377
```
加入到集群中去.

4、在61服务器上查看集群节点
```bash
[root@nodeb1 ~]# docker node list
ID                            HOSTNAME            STATUS              AVAILABILITY        MANAGER STATUS      ENGINE VERSION
0uh5qnbrold54jt64nylhwsmp *   nodeb1              Ready               Active              Leader              19.03.8
n92uz26razgw2mpq0nvk55mqk     nodeb2              Ready               Active                                  19.03.5
```
