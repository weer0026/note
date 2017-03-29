# 安装阶段

1. 安装virtualBox

2. （后面证明安装docker tools就好了）安装boot2docker `brew install boot2docker`,这里安装的时候会把docker一起安装好，因为boot2docker需要docker。

   安装完成以后，使用`boot2docker init`命令初始化，提示命令行执行方式不被推荐了，推荐时候docker tools来管理，所以下一步。

3. 下载安装docker tools，这里是用了kitematic的docker GUI，以后再去熟悉命令行，安装的时候出现下载不了boot2docker.iso的问题，我去github上下载了一份放到 `~/.docker`里面就好了。

   [ISO镜像](https://github.com/boot2docker/boot2docker/releases)

   `https://github.com/boot2docker/boot2docker/releases`

   ![kitematic的截图](https://ooo.0o0.ooo/2017/03/29/58db2547eadc4.png)

   *GUI界面*

   ​