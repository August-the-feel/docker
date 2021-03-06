# docker

1. 先进行复制nginx.conf文件 放到 ...(替换为自己路径和.env中的路径一致)/docker/nginx 目录下面 
```dockerfile
 docker run --name nginx -itd nginx:latest 
 docker cp nginx:/etc/nginx/ ...(替换为自己路径和.env中的路径一致)/docker/nginx
```

将 nginx.conf 放到docker/nginx的根目录下 其他文件删除掉

运行 

```dockerfile
 docker compose up -d 
```

mysql 远程连接设置

```mysql
# docker logs (mysql容器名称) 2>&1 | grep GENERATED
# docker exec -it  (mysql容器名称) bash
# mysql -uroot -p
# ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '自定义密码';
# flush privileges;
# CREATE USER 'root'@'%' IDENTIFIED BY '自定义密码';
# GRANT ALL ON *.* TO 'root'@'%';
# flush privileges;
```

redis 连接测试

```redis
redis-cli
```

```dockerfile
version: "3"
services:
  mariadb:
    image: mariadb
    hostname: mariadb
    privileged: true
    volumes:
      - ./mariadb:/var/lib/mysql/
    command:
      --character-set-server=utf8mb4
      --collation-server=utf8mb4_general_ci
      --transaction-isolation=READ-COMMITTED
      --binlog-format=ROW
      --innodb-file-per-table=1
      --skip-innodb-read-only-compressed
    environment:
      TZ: Asia/Shanghai
      MYSQL_ROOT_PASSWORD: qwer1234
    ports:
      - "3306:3306"
    restart: always
```

```dockerfile
version: "3"
services:
  mysql:
    image: mysql/mysql-server:latest
    hostname: mysql
    privileged: true
    volumes:
      - ./mysql:/var/lib/mysql/
      - ./mysql-files:/var/lib/mysql-files/
    command:
      --character-set-server=utf8mb4
      --collation-server=utf8mb4_general_ci
      --transaction-isolation=READ-COMMITTED
      --binlog-format=ROW
      --innodb-file-per-table=1
    environment:
      TZ: Asia/Shanghai
    ports:
      - "3306:3306"
    restart: always
# docker logs (mysql容器名称) 2>&1 | grep GENERATED
# docker exec -it  (mysql容器名称) bash
# mysql -uroot -p
# ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY '自定义密码';
# flush privileges;
# CREATE USER 'root'@'%' IDENTIFIED BY '自定义密码';
# GRANT ALL ON *.* TO 'root'@'%';
# flush privileges;
```

