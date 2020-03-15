# install\_nexus

## 一  简介:

```text
    Maven是一个纯java编写的开源项目管理工具，所有的项目配置信息都被定义在一个 POM.XML 的文件中,通过该文件 Maven 可以管理项目的整个生命周期,
        包括 清除、编译、测试、报告、打包、部署等等.目前 Apache 下的项目绝大多数已经采用了 Maven 进行管理. 
```

## 二  私服应用场景:

* 当多人协同开发的情况下,公司自己内部的 jar 包不容易管理.
* 公司内部的开发的公共组件不想被外网用户访问到,所以需要将 jar 包放在自己的服务器上.

## 三  linux之安装maven:

```text
    下载:               
        * wget http://mirror.bit.edu.cn/apache/maven/maven-3/3.5.2/binaries/apache-maven-3.5.2-bin.tar.gz
        * tar -zxvf apache-maven-3.5.2-bin.tar.gz
        * mv apache-maven-3.5.2 /usr/local/maven3.5
    配置环境变量:                    
        * vim /etc/profile
           在最后加上
        #maven                
        MAVEN_HOME=/usr/local/maven3.5               
        export MAVEN_HOME                      
        export PATH=${PATH}:${MAVEN_HOME}/bin         
    然后在使用命名让配置信息生效:
        source /etc/profile                     
    查看是否安装成功:
        mvn -v           
```

## 四  部署Nexus:

```text
    访问官网文档:
        https://www.sonatype.com/oss-thank-you-tar.gz               
        * 下载链接: http://nexus.sonatype.org/downloads/       
        * tar -zxvf  nexus.tar.gz                  
        * mv nexus-3.6.0-02 /usr/local/              
        * cd /usr/local/nexus-3.6.0-0.2/bin   
```

## 五  启动:

* ./nexus start
* 查看日志是否启动成功.

  注意: 访问的时候查看配置文件中的信息,一定要看. 配置文件中有访问路径和访问的 IP, 默认的用户名: admin 密码: admin123    

## 六 elipse 上传和下载 jar 到私服:

[_服务端 pom 配置:_](https://github.com/lidong320321/back-end/wiki/nexus%E4%B9%8B%E6%9C%8D%E5%8A%A1%E7%AB%AF-pom)    
__[依赖项目 pom 配置:](https://github.com/lidong320321/back-end/wiki/nexus%E4%B9%8B%E4%BE%9D%E8%B5%96%E9%A1%B9%E7%9B%AEpom)  
\*[settings 配置 :](https://github.com/lidong320321/back-end/wiki/nexus%E4%B9%8Bsettings%E9%85%8D%E7%BD%AE)

## 七 使用命令将 jar 包部署到服务器上：

deploy -e

