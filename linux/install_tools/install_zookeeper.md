# install\_zookeeper

1. 将下载好的安装包传到服务器上.
2. 解压文件:
   * tar -zxvf 文件名称
3. 将 conf 下的zoo\_sample.cfg 改名为 zoo.cfg
   * mv zoo\_sample.cfg ./zoo.cfg
4. 在文件解压的目录创建两个文件夹:
   * mkdir data
   * mkdir dataLog
5. 修改 zoo.cfg 中的配置:
   * vi zoo.cfg
   * dataLogDir=~/dataLog
   * dataDir=~/data
6. 启动服务:
   * cd  /home/ec2-user/zookeeper-3.4.8/bin/ 
   * sudo ./zkServer.sh start

