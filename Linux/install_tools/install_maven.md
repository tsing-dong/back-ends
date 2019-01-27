一、下载
```　　
        1.创建下载软件包目录
            mkdir /home/install
        2.在/home/install下载maven包，或者将下载好的maven压缩包上传至/home/install
            wget https://archive.apache.org/dist/maven/maven-3/3.5.4/binaries/apache-maven-3.5.4-bin.tar.gz
```
二、解压
```
        1.创建解压目录
　　        mkdir /usr/local/maven

        2.解压至/usr/local/maven/
            tar -zxvf apache-maven-3.5.4-bin.tar.gz -C /usr/local/maven/
```

三、配置环境变量
```　　    
        1.编辑/etc/profile
　　        vim /etc/profile

　　    2.在/etc/profile最后面追加以下代码
            MAVEN_HOME=/usr/local/maven/apache-maven-3.5.4
            PATH=$MAVEN_HOME/bin:$PATH
            export MAVEN_HOME PATH
```

        3.生效环境变量
```            
            source /etc/profile
```
        4.查看
```　　
            mvn -v
```
　　