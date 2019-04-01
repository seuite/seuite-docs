## 修改管理员密码
先进入Mariadb容器
```
 $ docker exec -it wiki-db -- mysql -uroot -p<mysql-root-password>
   mysql> use mediawiki;
```
查看wiki用户
```
    mysql> select * from user;
```
修改管理员密码
```
    mysql> UPDATE user SET user_password = MD5( CONCAT( user_id, '-', MD5( 'NEWPASS' ) ) ) WHERE user_id =1;
```