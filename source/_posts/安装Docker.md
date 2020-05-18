---
title: 安装Docker
comments: true
categories:
  - Docker
tags:
  - Docker
abbrlink: adt7e5ef
date: 2020-01-20 16:02:06
---

# Linux

> Docker — 从入门到实践
https://yeasy.gitbooks.io/docker_practice/content/
https://juejin.im/post/5cce4b1cf265da0373719819

详细的分步骤的安装说明可以参见官方文档，https://docs.docker.com/engine/installation/linux/ubuntu/

在官方文档中详细说明了不同Linux系统的安装方法，安装流程根据文档一步步执行即可安装成功。

但是为了使得安装更加方便，Docker官方还提供了一键安装脚本，使用它会使得安装更加便捷，不用再去一步步执行命令安装了，在此介绍一下一键脚本安装方式。

首先是Docker官方提供的安装脚本，相比其他脚本，官方提供的一定更靠谱，安装命令如下：

```
curl -sSL https://get.docker.com/ | sh
```

> 在安装过程中会出现`sudo usermod -aG docker your-user`只需要把`your-user`改成你当前的用户。

*将当前用户加入到docker用户组中*
```
sudo usermod -aG docker your-user
```
*重新启动docker服务或者重新登录终端再运行docker命令*
```
sudo service docker restart
```

只要执行如上一条命令，等待一会儿Docker便会安装完成，非常方便。

但是官方脚本安装有一个缺点，那就是慢，也可能下载超时，所以为了加快下载速度，我们可以使用国内的镜像来安装，所以在这里还有DaoCloud的安装脚本。

- DaoCloud安装脚本：
```
curl -sSL https://get.daocloud.io/docker | sh
```

等待脚本执行完毕之后，就可以使用Docker相关命令了，如运行测试Hello World镜像：

```
docker run hello-world
```

运行结果：

```
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
1b930d010525: Pull complete 
Digest: sha256:4fe721ccc2e8dc7362278a29dc660d833570ec2682f4e4194f4ee23e415e1064
Status: Downloaded newer image for hello-world:latest
```
如果出现上文类似提示内容则证明Docker可以正常使用了。


## 一、删除Docker镜像

> 在删除镜像前需要先删除docker，因为该image被对应的container引用，所以image删除失败

```
[root@VM_0_12_centos app]# docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
node                8-slim              9cd4d5af4312        8 days ago          146MB
hello-world         latest              fce289e99eb9        12 months ago       1.84kB
```
**1. 主要希望删除这两个imgae,根据image的id到container中找(由于已经删了是空的)**

```
[root@VM_0_12_centos app]# docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                   PORTS               NAMES
1c3632d52e9f        node:8-slim         "docker-entrypoint.s…"   3 hours ago         Exited (0) 3 hours ago                       sweet_feynman
0f6128a6443e        node:8-slim         "docker-entrypoint.s…"   3 hours ago         Exited (0) 3 hours ago                       determined_aryabhata
45aff5568711        hello-world         "/hello"                 4 hours ago         Exited (0) 4 hours ago 
```
删除
```
[root@VM_0_12_centos app]# docker rm 0f6128a6443e
0f6128a6443e
```

**2. 现在就可以删除docker了**

```
docker rmi 9cd4d5af4312
```

*官方建议的批量删除停止容器使用`docker rm $(sudo docker ps -a -q)`*

*千万不要用 `docker rm -f $(sudo docker ps -a -q)`,会删除全部容器的*

> 1、删除所有容器`docker rm docker ps -a -q`\
2、删除所有镜像 `docker rmi docker images -q`

[引用Docker 删除镜像](https://www.cnblogs.com/sddai/p/10427785.html)

3. 修改容器名字
    - 修改容器(第一个参数可以是name和id)
https://docs.docker.com/engine/reference/commandline/rename/
```
docker ps -a

docker rename <my_container> <my_new_container>
```

# 二、进入容器
**1. 进入容器内部**
```
[root@VM_0_12_centos ~]# docker exec -ti wepy/mall /bin/bash
```

**2.docker安装nginx静态文件服务器**
https://blog.csdn.net/wugenqiang/article/details/86513257

# 三、Dockerfile配置
![](http://img.cdn.vmccc.cn/16ead7303985b8fd.png)

# 参数对应
- docker run 基于镜像启动一个容器
- -p 3000:80 端口映射，将宿主的3000端口映射到容器的80端口
- -d 后台方式运行
- --name 容器名 查看 docker 进程