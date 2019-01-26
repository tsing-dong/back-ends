1. 将安装包传到服务器指定的安装目录．
2. 解压压缩包.
    * 命令: tar -zxvf jdk的名字
3. 配置环境变量:
    * 切换目录:
        cd /etc
    * 编辑文档:
        vim  profile 
    * 切换到最后一行:
        G
    *  
       ```
       配置环境变量:
       export JAVA_HOME=/usr/lib/jvm/jdk1.8.0_131  
       export JRE_HOME=${JAVA_HOME}/jre  
       export CLASSPATH=.:${JAVA_HOME}/lib:${JRE_HOME}/lib  
       export  PATH=${JAVA_HOME}/bin:$PATH
       ```
4. 重新加载配置文件,使刚才配置的信息生效
     * sources /etc/profile
5.  使用命令检查是否安装成功:
      * java  -version 