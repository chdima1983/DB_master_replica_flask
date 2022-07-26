## Homework DB (master-replica) with my Flask


### Make this in MYSQL database in master instance
```
CREATE USER 'replica'@'172.31.%.%' IDENTIFIED WITH mysql_native_password BY 'VeryStrongwith$%^andLongPassword';
GRANT REPLICATION SLAVE ON *.* TO 'replica'@'172.31.%.%';
FLUSH PRIVILEGES;
```

SHOW MASTER STATUS\G

Take your values like these:
```
File: mysql-binlog.000001
Position: 851
```

#Make this in MYSQL database in replica instance with your data.
```
CHANGE MASTER TO MASTER_HOST='172.31.36.226' ,
    MASTER_USER='replica' ,
    MASTER_PASSWORD='VeryStrongwith$%^andLongPassword' ,
    MASTER_LOG_FILE='mysql-binlog.000001' ,
    MASTER_LOG_POS=851;
```

START REPLICA;

SHOW REPLICA STATUS\G
