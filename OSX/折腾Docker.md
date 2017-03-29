# 安装阶段

1. 安装virtualBox

2. （后面证明安装docker tools就好了）安装boot2docker `brew install boot2docker`,这里安装的时候会把docker一起安装好，因为boot2docker需要docker。

   安装完成以后，使用`boot2docker init`命令初始化，提示命令行执行方式不被推荐了，推荐时候docker tools来管理，所以下一步。

3. 下载安装docker tools，这里是用了kitematic的docker GUI，以后再去熟悉命令行，安装的时候出现下载不了boot2docker.iso的问题，我去github上下载了一份放到 `~/.docker`里面就好了。

   [ISO镜像](https://github.com/boot2docker/boot2docker/releases)

   `https://github.com/boot2docker/boot2docker/releases`

   ![kitematic的截图](https://ooo.0o0.ooo/2017/03/29/58db2547eadc4.png)

   *GUI界面*

### 命令行折腾

##### 查看目前的镜像

`docker image ls`

![出错的截图](https://ooo.0o0.ooo/2017/03/29/58db2c26c5daf.png)

然后我报错了，因为我没有设置好环境参数

>*安装完docker以后还需要设置一些参数*
>
>` $ docker-machine start //开启虚拟机`
>
> `$ docker-machine env  //查看下环境变量的设置`
>
>`$ eval "$(docker-machine env default)" //设置默认的环境变量`

正确的返回

![正确返回结果](https://ooo.0o0.ooo/2017/03/29/58db2c26d662d.png)



### 小结

看了不少文档，总结一下个人对docker的理解。

例如搭建一个php + mysql + nginx的开发环境，正常工作流程就是在自己的电脑上分别安装部署，但是平时工作中都会遇到更新版本（升级php版本等）的问题，使用docker一方面可以使用共有仓库的配置，另一个方面就是docker推崇的但进程服务，把php,mysql,nginx分拆成单个的docker容器，在使用时进行链接，可以做到平滑切换版本。