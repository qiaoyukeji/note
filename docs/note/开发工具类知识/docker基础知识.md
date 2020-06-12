<!--
 * @Descripttion: 
 * @version: 
 * @Author: qiaoyurensheng@163.com
 * @Date: 2020-06-13 03:02:41
 * @LastEditors: Please set LastEditors
 * @LastEditTime: 2020-06-13 03:03:13
--> 
<!-- ## docker学习笔记（黑马）—— 2020.03 -->
## docker学习笔记
### 1、安装docker
```bash
# 1、yum 包更新到最新 
yum update
# 2、安装需要的软件包， yum-util 提供yum-config-manager功能，另外两个是devicemapper驱动依赖的 
yum install -y yum-utils device-mapper-persistent-data lvm2
# 3、 设置yum源
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
# 4、 安装docker，出现输入的界面都按 y 
yum install -y docker-ce
# 5、 查看docker版本，验证是否验证成功
docker -v
```

### 2、配置镜像加速（使用aliyun）
```bash
# 在阿里云网站的镜像服务里
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://q5cacvhb.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```
### 3、基础命令
```bash
# 启动docker
systemctl start docker

# 查看docker状态
systenctl status docker

# 关闭docker
systemctl stop docker

# 重启docker
systemctl restart docker

# 设置开机启动docker服务
systemctl enable docker
```

### 4、镜像相关命令
```bash
# 查看镜像: 查看本地所有的镜像
docker images
docker images –q # 查看所用镜像的id

# 搜索镜像:从网络中查找需要的镜像
docker search 镜像名称

# 拉取镜像:从Docker仓库下载镜像到本地，镜像名称格式为 名称:版本号，如果版本号不指定则是最新的版本。如果不知道镜像版本，可以去docker hub 搜索对应镜像查看。
docker pull 镜像名称
docker pull 镜像名称:版本号

# 删除镜像: 删除本地镜像
docker rmi 镜像id # 删除指定本地镜像
docker rmi 镜像名称:版本号 # 删除指定版本的本地镜像
docker rmi `docker images -q`  # 删除所有本地镜像

```

### 5、容器相关命令
```bash
# 查看容器
docker ps # 查看正在运行的容器
docker ps –a # 查看所有容器

# 创建并启动容器
docker run 参数  镜像名称:版本号
例：docker run -i -t --name=c1 centos:7 /bin/bash

# 参数说明:
# -i：保持容器运行。通常与 -t 同时使用。加入it这两个参数后，容器创建后自动进入容器中，退出容器后，容器自动关闭。
# -t：为容器重新分配一个伪输入终端，通常与 -i 同时使用。
# -d：以守护（后台）模式运行容器。创建一个容器在后台运行，需要使用docker exec 进入容器。退出后，容器不会关闭。
# -it 创建的容器一般称为交互式容器，-id 创建的容器一般称为守护式容器
# --name：为创建的容器命名。

# 进入容器
docker exec 参数  容器名称  
例：docker exec -it c1 /bin/bash

# 停止容器
docker stop 容器名称

# 启动容器
docker start 容器名称

# 删除容器：如果容器是运行状态则删除失败，需要停止容器才能删除
docker rm 容器名称

# 查看容器信息
docker inspect 容器名称


```

### 6、容器的数据卷

> 数据卷：  
>> - 数据卷是宿主机中的一个目录  
>> - 当容器目录和数据卷绑定后，对方的修改会立即同步  
>> - 一个数据卷可以被多个容器挂在  
>> - 一个容器也可以挂载多个数据卷  
>
> 注意事项：
>> 1.目录必须为绝对目录  
>> 2.如果目录不存在，会自动创建  
>> 3.可以挂载多个数据卷




配置数据卷:
```bash
# 创建启动容器时，使用-v参数设置数据卷
docker run ... -v 宿主机目录(文件):容器内目录(文件) ...
例：docker run -it --name=c2 -v /root/data2:/root/data2 -v /root/data3:/root/data3 centos:7
```
多容器进行数据交换：  
- 1.多容器挂载同一个数据卷
- 2.数据卷容器  

数据卷容器:
```bash
# 1.创建启动c3数据卷容器，使用 –v 参数(可更改目录名) 设置数据卷
docker run –it --name=c3 –v /volume centos:7 /bin/bash 

# 2.创建启动 c1 c2 容器，使用 –-volumes-from 参数 设置数据卷
docker run –it --name=c1 --volumes-from c3 centos:7 /bin/bash

docker run –it --name=c2 --volumes-from c3 centos:7 /bin/bash  

```
#### 小结：

1.数据卷概念
- 宿主机的一个目录或文件  

2.数据卷作用
- 容器数据持久化
- 客户端和容器数据交换
- 容器间数据交换

3.数据卷容器
- 创建一个容器，挂载一个目录，让其他容器继承自该容器( --volume-from )。
- 通过简单方式实现数据卷配置


### 7、docker的应用部署

> #### mysql的部署


1. 搜索mysql镜像

```bash
docker search mysql
```

2. 拉取mysql镜像

```bash
docker pull mysql:5.6
```

3. 创建容器，设置端口映射、目录映射

```bash
# 在/root目录下创建mysql目录用于存储mysql数据信息
mkdir ~/mysql
cd ~/mysql
```

```bash
docker run -id \
-p 3307:3306 \
--name=c_mysql \
-v $PWD/conf:/etc/mysql/conf.d \
-v $PWD/logs:/logs \
-v $PWD/data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=123456 \
mysql:5.6
```

- 参数说明：
  - **-p 3307:3306**：将容器的 3306 端口映射到宿主机的 3307 端口。
  - **-v $PWD/conf:/etc/mysql/conf.d**：将主机当前目录下的 conf/my.cnf 挂载到容器的 /etc/mysql/my.cnf。配置目录
  - **-v $PWD/logs:/logs**：将主机当前目录下的 logs 目录挂载到容器的 /logs。日志目录
  - **-v $PWD/data:/var/lib/mysql** ：将主机当前目录下的data目录挂载到容器的 /var/lib/mysql 。数据目录
   - **-e MYSQL_ROOT_PASSWORD=123456：**初始化 root 用户的密码。

4. 进入容器，操作mysql

```bash
docker exec –it c_mysql /bin/bash
```

> #### Tomcat的部署

1. 搜索tomcat镜像

```bash
docker search tomcat
```

2. 拉取tomcat镜像

```bash
docker pull tomcat
```

3. 创建容器，设置端口映射、目录映射

```bash
# 在/root目录下创建tomcat目录用于存储tomcat数据信息
mkdir ~/tomcat
cd ~/tomcat
```

```bash
docker run -id --name=c_tomcat \
-p 8080:8080 \
-v $PWD:/usr/local/tomcat/webapps \
tomcat 
```

- 参数说明：
  - **-p 8080:8080：**将容器的8080端口映射到主机的8080端口
  
  -  **-v $PWD:/usr/local/tomcat/webapps：**将主机中当前目录挂载到容器的webapps

> #### Nginx的部署
1. 搜索nginx镜像

```bash
docker search nginx
```

2. 拉取nginx镜像

```bash
docker pull nginx
```

3. 创建容器，设置端口映射、目录映射


```bash
# 在/root目录下创建nginx目录用于存储nginx数据信息
mkdir ~/nginx
cd ~/nginx
mkdir conf
cd conf
# 在~/nginx/conf/下创建nginx.conf文件,粘贴下面内容
vim nginx.conf
```
```bash

user  nginx;
worker_processes  1;

error_log  /var/log/nginx/error.log warn;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;
}


```

```bash
docker run -id --name=c_nginx \
-p 80:80 \
-v $PWD/conf/nginx.conf:/etc/nginx/nginx.conf \   # $PWD为/root/nginx
-v $PWD/logs:/var/log/nginx \
-v $PWD/html:/usr/share/nginx/html \
nginx
```

- 参数说明：
  - **-p 80:80**：将容器的 80端口映射到宿主机的 80 端口。
  - **-v $PWD/conf/nginx.conf:/etc/nginx/nginx.conf**：将主机当前目录下的 /conf/nginx.conf 挂载到容器的 :/etc/nginx/nginx.conf。配置目录
  - **-v $PWD/logs:/var/log/nginx**：将主机当前目录下的 logs 目录挂载到容器的/var/log/nginx。日志目录

> #### redis的部署
1. 搜索redis镜像

```bash
docker search redis
```

2. 拉取redis镜像

```bash
docker pull redis:5.0
```

3. 创建容器，设置端口映射

```bash
docker run -id --name=c_redis -p 6379:6379 redis:5.0
```

4. 使用外部机器连接redis

```bash
./redis-cli.exe -h 192.168.149.135 -p 6379
```

### 8、Dockerfile
- Docker镜像原理
  - docker镜像是由特殊的文件系统叠加而成
  - 最底层是bootfs，并使用宿主机的bootfs
  - 第二层是 root文件系统rootfs，称为base image
  - 然后再往上可以叠加其他的镜像文件
  - 统一文件系统（Union File System）技术能够将不同的层整合成一个文件系统，为这些层提供了一个统一的视角，这样就隐藏了多层的存在，在用户的角度看来，只存在一个文件系统。 
  - 一个镜像可以放在另一个镜像的上面。位于下面的镜像称为父镜像，最底部的镜像成为基础镜像。
  - 当从一个镜像启动容器时，Docker会在最顶层加载一个读写文件系统作为容器

- 镜像制作
  - 1、容器转镜像  
    ```bash
    docker commit 容器id 镜像名称:版本号

    #压缩打包镜像文件
    docker save -o 压缩文件名称 镜像名称:版本号
    
    #解压镜像文件
    docker load -i 压缩文件名称
    ```
  - 2、Dockerfile
    > - Dockerfile 是一个文本文件  
    >        - 包含了一条条的指令  
    > - 每一条指令构建一层，基于基础镜像，最终构建出一个新的镜像  
    > - 对于开发人员：可以为开发团队提供一个完全一致的开发环境  
    > - 对于测试人员：可以直接拿开发时所构建的镜像或者通过Dockerfile文件构建个新的镜像开始工作了
    > - 对于运维人员：在部署时，可以实现应用的无缝移植
  
  - 3 、Dockerfile编写步骤
      - 1.Docker 构建部署 centos + vim
        + 定义父镜像：FROM centos:7   
        + 定义作者信息：MAINTAINER  itheima <itheima@itcast.cn>  
        + 执行安装vim命令： RUN yum install -y vim  
        + 定义默认的工作目录：WORKDIR /usr  
        + 定义容器启动执行的命令：CMD /bin/bash  
          ```bash
          #通过dockerfile构建镜像：
          docker bulid –f dockerfile文件路径 –t 镜像名称:版本  
          ```
      - 2.Dockerfile 构建部署 springboot 项目案例  
        + 定义父镜像：FROM java:8
        + 定义作者信息：MAINTAINER  itheima <itheima@itcast.cn>
        + 将jar包添加到容器： ADD springboot.jar app.jar
        + 定义容器启动执行的命令：CMD java–jar app.jar
        ```bash
        # 通过dockerfile构建镜像：
        docker bulid –f dockerfile文件路径 –t 镜像名称:版本
        ```

[ 注 ]：docker制作镜像的一些关键字

| 关键字      | 作用                     | 备注                                                                                                                        |
| ----------- | ------------------------ | --------------------------------------------------------------------------------------------------------------------------- |
| FROM        | 指定父镜像               | 指定dockerfile基于那个image构建                                                                                             |
| MAINTAINER  | 作者信息                 | 用来标明这个dockerfile谁写的                                                                                                |
| LABEL       | 标签                     | 用来标明dockerfile的标签 可以使用Label代替Maintainer 最终都是在docker image基本信息中可以查看                               |
| RUN         | 执行命令                 | 执行一段命令 默认是/bin/sh 格式: RUN command 或者 RUN ["command" , "param1","param2"]                                       |
| CMD         | 容器启动命令             | 提供启动容器时候的默认命令 和ENTRYPOINT配合使用.格式 CMD command param1 param2 或者 CMD ["command" , "param1","param2"]     |
| ENTRYPOINT  | 入口                     | 一般在制作一些执行就关闭的容器中会使用                                                                                      |
| COPY        | 复制文件                 | build的时候复制文件到image中                                                                                                |
| ADD         | 添加文件                 | build的时候添加文件到image中 不仅仅局限于当前build上下文 可以来源于远程服务                                                 |
| ENV         | 环境变量                 | 指定build时候的环境变量 可以在启动的容器的时候 通过-e覆盖 格式ENV name=value                                                |
| ARG         | 构建参数                 | 构建参数 只在构建的时候使用的参数 如果有ENV 那么ENV的相同名字的值始终覆盖arg的参数                                          |
| VOLUME      | 定义外部可以挂载的数据卷 | 指定build的image那些目录可以启动的时候挂载到文件系统中 启动容器的时候使用 -v 绑定 格式 VOLUME ["目录"]                      |
| EXPOSE      | 暴露端口                 | 定义容器运行的时候监听的端口 启动容器的使用-p来绑定暴露端口 格式: EXPOSE 8080 或者 EXPOSE 8080/udp                          |
| WORKDIR     | 工作目录                 | 指定容器内部的工作目录 如果没有创建则自动创建 如果指定/ 使用的是绝对地址 如果不是/开头那么是在上一条workdir的路径的相对路径 |
| USER        | 指定执行用户             | 指定build或者启动的时候 用户 在RUN CMD ENTRYPONT执行的时候的用户                                                            |
| HEALTHCHECK | 健康检查                 | 指定监测当前容器的健康监测的命令 基本上没用 因为很多时候 应用本身有健康监测机制                                             |
| ONBUILD     | 触发器                   | 当存在ONBUILD关键字的镜像作为基础镜像的时候 当执行FROM完成之后 会执行 ONBUILD的命令 但是不影响当前镜像 用处也不怎么大       |
| STOPSIGNAL  | 发送信号量到宿主机       | 该STOPSIGNAL指令设置将发送到容器的系统调用信号以退出。                                                                      |
| bash        | 指定执行脚本的bash       | 指定RUN CMD ENTRYPOINT 执行命令的时候 使用的bash                                                                            |

---

### 9、Docker Compose

- 安装docker compose
  ```bash
    # Compose目前已经完全支持Linux、Mac OS和Windows，在我们安装Compose之前，需要先安装Docker。下面我 们以编译好的二进制包方式安装在Linux系统中。   
    curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
    # 设置文件可执行权限 
    chmod +x /usr/local/bin/docker-compose
    # 查看版本信息 
    docker-compose -version
  ```

- 创建docker-compose目录

  ```bash
  mkdir ~/docker-compose
  cd ~/docker-compose
  ```

- 编写 docker-compose.yml 文件

  ```bash
  version: '3'
  services:
    nginx:
    image: nginx
    ports:
      - 80:80
    links:
      - app
    volumes:
      - ./nginx/conf.d:/etc/nginx/conf.d
    app:
      image: app
      expose:
        - "8080"
  ```

- 创建./nginx/conf.d目录

  ```bash
  mkdir -p ./nginx/conf.d
  ```

- 在./nginx/conf.d目录下 编写itheima.conf文件

  ```bash
  server {
      listen 80;
      access_log off;

      location / {
          proxy_pass http://app:8080;
      }
    
  }
  ```

- 在~/docker-compose 目录下 使用docker-compose 启动容器

  ```bash
  docker-compose up
  ```

### 10、docker私有仓库
- 私有仓库搭建
  ```bash
  # 1、拉取私有仓库镜像 
  docker pull registry
  # 2、启动私有仓库容器 
  docker run -id --name=registry -p 5000:5000 registry
  # 3、打开浏览器 输入地址http://私有仓库服务器ip:5000/v2/_catalog，看到{"repositories":[]} 表示私有仓库 搭建成功
  # 4、修改daemon.json   
  vim /etc/docker/daemon.json    
  # 在上述文件中添加一个key，保存退出。此步用于让 docker 信任私有仓库地址；注意将私有仓库服务器ip修改为自己私有仓库服务器真实ip 
  {"insecure-registries":["私有仓库服务器ip:5000"]} 
  # 5、重启docker 服务 
  systemctl restart docker
  docker start registry

  ```

- 将镜像上传至私有仓库

  ```bash
  # 1、标记镜像为私有仓库的镜像     
  docker tag centos:7 私有仓库服务器IP:5000/centos:7
  
  # 2、上传标记的镜像     
  docker push 私有仓库服务器IP:5000/centos:7

  ```
  
- 从私有仓库拉取镜像 

  ```bash
  #拉取镜像 
  docker pull 私有仓库服务器ip:5000/centos:7
  ```