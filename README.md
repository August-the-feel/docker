# docker

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

