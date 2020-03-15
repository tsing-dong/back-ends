# basicKnowledge\_application

## 1. 创建用户并且给用户赋权限

> 1. 查询数据库的所有用户信息:

eg:

```text
    SELECT HOST,USER,authentication_string FROM mysql.user;
```

> 1. 创建用户:

语法:

```text
    create user "username"@"host" identified by "password";
```

eg:

```sql
1.mysql->create user 'test'@'localhost' identified by '123';

2.mysql->create user 'test'@'192.168.7.22' identified by '123';

3.mysql->create user 'test'@'%' identified by '123';

4. mysql-> CREATE USER 'test_user_service'@'%' IDENTIFIED BY 'Li15150594533.';
```

/_host="localhost"为本地登录用户，host="ip"为ip地址登录，host="%"，为外网ip登录_/

> 1. 创建数据库:

eg:

```text
      CREATE DATABASE test_database;
```

> 1. 给用户设置指定可以访问的数据库:

eg:

```text
    GRANT ALL PRIVILEGES ON  test_database.* TO 'test_user_service'@'%';
```

> 1. 刷新权限:
>
>    ```text
>     flush privileges;
>    ```

## 2. 客户端链接数据库时,数据库报密码乱码的问题:

> 1. 修改加密规则:
>
>    > ALTER USER 'product\_service'@'%' IDENTIFIED BY 'Li15150594533.' PASSWORD EXPIRE NEVER;
>
> 2. 更新用户的密码:
>
>    > ALTER USER 'product\_service'@'%' IDENTIFIED WITH mysql\_native\_password BY 'Li15150594533.';
>
> 3. 重置一下密码:
>
>    > ALTER USER 'product\_service'@'%' IDENTIFIED BY 'Li15150594533.';
>
> 4. 刷新配置:
>
>    > FLUSH PRIVILEGES;

