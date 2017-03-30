###  用Docker搭建我的php开发环境

1. 创建Mysql容器

   > MySQL继承自官方的[MySQL5.6镜像](https://registry.hub.docker.com/_/mysql)，Dockerfile仅有一行，无需做任何额外处理，因为普通需求官方都已经在镜像中实现了，因此Dockerfile的内容为：
   >
   > ```
   > FROM mysql:5.6
   > ```
   >
   > 在项目根目录下运行
   >
   > ```
   > docker build -t eva/mysql ./mysql
   >
   > ```
   >
   > 会自动下载并构建镜像，这里我们将其命名为`eva/mysql`。
   >
   > 由于容器运行结束时会丢弃所有数据库数据，为了不用每次都要导入数据，我们将采用挂载的方式持久化MySQL数据库，官方镜像默认将数据库存放在`/var/lib/mysql`，同时要求容器运行时必须通过环境变量设置一个管理员密码，因此可以使用以下指令运行容器：
   >
   > ```
   > docker run -p 3306:3306 -v ~/opt/data/mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -it eva/mysql
   >
   > ```
   >
   > 通过上面的指令，我们将本地的3306端口绑定到容器的3306端口，将容器内的数据库持久化到本地的`~/opt/data/mysql`，并且为MySQL设置了一个root密码`123456`

   按照网上的教程走，有一个小问题就是权限不够，解决方法是在Dockerfile里面添加代码来修改目录的权限：

   ```
   RUN deluser mysql
   RUN useradd mysql
   RUN mkdir -p /Users/me/docker/mysql/data
   RUN chmod -R 777 /Users/me/docker/mysql/data
   ```

   然后就可以运行成功了。

2. nginx

3. php

4. redis

5. 将所有容器链接起来

   使用docker-compose工具进行操作，首先安装docker-compose

   `sudo pip -U docker-compose //使用sudo是因为我当前用户没有操作/usr/bin目录的权限`

   安装完成可以使用`docker-compose --version` 查看是否成功，但是我有bug体质，一看果然报错。

   ![docker-compose报错截图](https://ooo.0o0.ooo/2017/03/30/58dc6b86a82a2.png)

   google以后找到了解决方案：[stackoverflow链接](http://stackoverflow.com/questions/27630114/matplotlib-issue-on-os-x-importerror-cannot-import-name-thread)，第二回答解决了我的问题，大致意思是我的电脑上的python2.7自带的six模块版本太旧，虽然安装了新的six模块，但是旧版本six模块还在，引用出错，删除掉老版本的six模块就好了。

   ![docker-compose正常安装截图](https://ooo.0o0.ooo/2017/03/30/58dc6c6be6c41.png)

6. 