# install\_redis

## 1. 下载

```text
     http://redis.io/download    
     wget http://download.redis.io/releases/redis-4.0.9.tar.gz           
```

## 2. 将下载的安装包传至服务器上

## 3.  安装

```text
      cd redis-2.8.17
      make      
      cd src
      make install PREFIX=/usr/local/redis
```

注意: make 编译失败,可能因为没有 gcc 服务

## 查看 gcc 是否安装成功

```text
      rep -qa|grep gcc          
```

## 4. 将配置文件移动到 redis 安装目录下

```text
      mv redis.conf /usr/local/redis/etc    
```

## 5. 启动服务

```text
      /usr/local/redis/bin/redis-server /usr/local/redis/etc/redis.conf
```

## 6. 默认情况下,redis 不是后台启动,设置后台启动

```text
      vim  redis.conf
      将daemonize的值改为yes
```

## 7. 让 redis 开机自启

```text
       vim /etc/rc.local
       加入
       /usr/local/redis/bin/redis-server /usr/local/redis/etc/redis-conf
```

## 8. 设置权限登录

```text
       1、注释掉redis安装目录下的redis.conf文件中的如下数据：bind 127.0.0.1，注释#bind 127.0.0.1   或者修改bind 0.0.0.0
       2、修改保护模式为非：默认为protected-mode yes ,修改后为protected-mode no
       3、设置redis连接密码：找到#requirepass foobared ,在下面添加requirepass 123456
```

## 带密码的命令行登录

```text
       带密码的启动方式
             ./redis-cli -h 127.0.0.1 -p 6379 -a 123456
             -h 是主机IP地址
             -p 是端口号
             -a 是密码
```

