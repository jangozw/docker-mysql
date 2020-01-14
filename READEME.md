docker-compose 创建mysql并初始化数据. 

原理是：

mysql 官方镜像入口脚本（建议了解) https://github.com/docker-library/mysql/blob/master/5.6/docker-entrypoint.sh
已经预留了/docker-entrypoint-initdb.d/目录供初始化数据


以下实例亲测成功！
# 版本
> mysql:  8.0.18

> docker-compose : docker-compose version 1.16.1, build 6d1ac21

> Docker version 18.06.1-ce, build e68fc7a


# 目录结构

```

├── .env  # 变量文件，在yml中可直接引用
├── docker-compose.yml
├── mysql  
│   ├── data # MYSQL 的所有数据便于备份
│   ├── conf # MYSQL 的配置同步挂载到容器
│   │   └── my.cnf  
│   └── scripts # MYSQL 容器初始化需要执行的数据，如项目数据表, 以.sql或.sh结尾就行
│       └── sql.sql
└── mysql.build # 构建mysql的镜像，里面将执行的初始化脚本导入
```

# 运行

```
# 如果修改了脚本或配置重新启动需要 docker-compose build --no-cache

docker-compose up
```
控制台结果
```
jang@jiangMacBook-Pro:~/www/go-projects/docker|
⇒  docker-compose up
Attaching to test_mysql
...

没有退出的话就ok
```

查看容器

```
⇒  docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                               NAMES
6bc30b1612f9        docker_mysql        "docker-entrypoint.s…"   33 seconds ago      Up 31 seconds       33060/tcp, 0.0.0.0:3310->3306/tcp   test_mysql
```

# 远程连接
打开数据库连接软件，输入配置的用户名密码，连接成功！


