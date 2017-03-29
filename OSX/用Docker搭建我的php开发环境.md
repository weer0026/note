###  用Docker搭建我的php开发环境

1. 创建Mysql容器

   > MySQL继承自官方的[MySQL5.6镜像](https://registry.hub.docker.com/_/mysql)，Dockerfile仅有一行，无需做任何额外处理，因为普通需求官方都已经在镜像中实现了，因此Dockerfile的内容为：
   >
   > ```
   > FROM mysql:5.6
   >
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