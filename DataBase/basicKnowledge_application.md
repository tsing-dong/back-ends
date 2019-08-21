# 1. 创建用户并且给用户赋权限
> 1. 查询数据库的所有用户信息:  

eg:
```
    SELECT HOST,USER,authentication_string FROM mysql.user;
```

> 2. 创建用户: 

语法:
```
    create user "username"@"host" identified by "password";
```

eg:
```sql
1.mysql->create user 'test'@'localhost' identified by '123';

2.mysql->create user 'test'@'192.168.7.22' identified by '123';

3.mysql->create user 'test'@'%' identified by '123';

4. mysql-> CREATE USER 'test_user_service'@'%' IDENTIFIED BY 'Li15150594533.';
```
  /*host="localhost"为本地登录用户，host="ip"为ip地址登录，host="%"，为外网ip登录*/


> 3. 创建数据库:

eg:

```
      CREATE DATABASE test_database;
```

> 4. 给用户设置指定可以访问的数据库:

eg:
```
    GRANT ALL PRIVILEGES ON  test_database.* TO 'test_user_service'@'%';
```

> 5. 刷新权限:
```
    flush privileges;
```