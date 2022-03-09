# docker

先进行docker run --name nginx -itd nginx:latest 
docker cp nginx:docker cp nginx:/etc/nginx/ /Users/zhangyuze/docker/nginx
将 nginx.conf 放到docker/nginx的根目录下

运行 docker compose up -d 

mysql 远程连接设置

```mysql
# docker logs mysql_mysql_1 2>&1 | grep GENERATED
# docker exec -it  mysql_mysql_1 bash
# mysql -uroot -p
# ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'qwer1234';
# flush privileges;
# CREATE USER 'root'@'%' IDENTIFIED BY 'qwer1234';
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
# docker logs mysql_mysql_1 2>&1 | grep GENERATED
# docker exec -it  mysql_mysql_1 bash
# mysql -uroot -p
# ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'qwer1234';
# flush privileges;
# CREATE USER 'root'@'%' IDENTIFIED BY 'qwer1234';
# GRANT ALL ON *.* TO 'root'@'%';
# flush privileges;
```

