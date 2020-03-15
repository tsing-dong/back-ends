# 1. Linux 中安装 mysql - rpm 方式安装\(下载速度较慢\)/这个是linux服务器上以前没安装过mysql 的服务:

> 1. 去 mysql 官网找到自己想要的 rpm 包,执行 : wget rpm的链接;
> 2. 安装: sudo rpm -ivh 下载的文件名;
> 3. sudo yum install mysql-server 安装完成
> 4. 启动 mysql 服务: systemctl start mysqld;
> 5. 找到密码: sudo grep 'temporary password' /var/log/mysqld.log
> 6. localhost：后面的就是密码
> 7. 配置安装项: sudo mysql\_secure\_installation 这个时候把刚才的密码粘贴过来,然后会让你填写新的密码,新密码的规则是: 总共8个字符 / 一个大写字母 + 一个小写字母 + 加一个特殊字符 + 数字 中间还有一些问题,自己填写 Y 或者 N 就可以了
> 8. 登录一下: mysql -uroot -p 加上密码;
> 9. 客户端工具连接的时候会报错,需要设置远程连接的权限: 如果是虚拟机 安装的 mysql 需要关闭防火墙,我是阿里云的所以在上面开放了 mysql 的端口就可以了
> 10. GRANT ALL PRIVILEGES ON _._ TO 'root'@'%'WITH GRANT OPTION;
> 11. 最后刷新一下配置: FLUSH PRIVILEGES;

