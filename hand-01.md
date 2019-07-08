# 日报
## 一.上午git
* 1.git是什么？
```
git是版本控制工具，简而言之，在企业开发中，团队之间系统开发所必需的。管理多人协同开发，
```
* 2.git和svn的区别？
```
最核心的区别是：git是分布式的，而svn不是分布式，

git完美的支持分支功能，svn虽然也支持，但是比较笨拙

svn有全局版本号，svn不具有
```
* 3.git常用操作：
```
l快速切换到上一个分支----->git checkout -

l别处本地和远程所有分支-----> git branch -a

l创建并切换到本地分支-----> git checkout -b "branch-name"

l查看commit历史----->git log

l列出所有远程仓库----->git remote

 [more git command link](https://github.com/521xueweihan/git-tips "With a Title"). 
```

---
## 二.下午linux/maven/docker

* linux基本命令
```
github有整理出来的平时常用操作的命令
 [more linux command link](https://github.com/guodongxiaren/LinuxTool "With a Title")```

```
* 1.docker是什么？
```
docker采用虚拟容器技术，将系统运行所需环境整合在容器中，实现进程隔离，更加有效地利用系统资源，相比虚拟机，它更加的轻巧灵活，能以更快的速度启动。docker摒弃了传统的开发模式，确保运行环境一致性，解放开发运维的双手。
```
2.三个基本概念
```
镜像（Image）
容器（Container）
仓库（Repository）

镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的类和实例一 样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、 暂停等。

容器的实质是进程，但与直接在宿主执行的进程不同，容器进程运行于属于自己的独立的命名空间。因此容器可以拥有自己的root文件系统自己的网络配置自己的进程空间，甚 至自己的用户ID空间。容器内的进程是运行在一个隔离的环境里，使用起来就好像是在一 个独立于宿主的系统下操作一样。这种特性使得容器封装的应用比直接在宿主运行更加安全。

仓库；即存放镜像的库

```
3docker基础指令：
```
3.1 docker ps
产看正在运行的docker容器：docker ps
重启docker容器：docker restart 容器id
3.2docker run
运行容器：bash docker	run	--name	webserver	-d	-p	80:80	nginx 
这条命令会用 nginx 镜像启动一个容器，命名为 webserver ，并且映射了 80	端口。
3.3 docker exec
进入容器bash docker	exec	-it	webserver	bash
这条命令用bash交互终端的方式获得一个可操作的shell进入了webserver
-it：（1）-i:交互式操作（2）-t：终端（3）-it：交互式终端
-rm： 容器退出后将其删除，避免浪费空间。默认不会立即删除，为排障需求
3.4 docker diff
查看具体在容器存储层的改动
3.5 docker history
查看镜像历史记录
3.6 docker images
查看docker容器日志：docker logs -f --tail 100 （容器name）/
3.7 docker logs -f --tail 100 mysql3306
3.8docker    pull	[选项]	[Docker	Registry地址]<仓库名>:<标签>
eg:docker pull ubuntu:14.04 

 ```