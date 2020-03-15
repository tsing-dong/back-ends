# 1. \(Ubuntu\)linux 中安装 nginx :

> 1. 安装依赖:
>
>    \`\`\`
>
>     sudo apt install gcc
>
>     sudo apt install  pcre-devel
>
>     sudo apt install  zlib zlib-devel
>
>     sudo apt install  openssl openssl-devel

```text
// 你以为会成功吗? 反正我没成功 ubuntu 18.* 中,安装 pcre-devel 会有问题:
//执行 
sudo apt install  libpcre3 libpcre3-dev 
```

\`\`\`

> 1. 下载 nginx 的 tar 包:
>
>    > 2.1 在 usr/local 创建一个文件夹:
>    >
>    > > sudo mkdir download\_nginx
>
> > 2.2 切换到创建的目录下:
> >
> > > cd download\_nginx
> >
> > 2.3 下载自己想要的版本:
> >
> > > wget [http://nginx.org/download/nginx-\*.tar.gz](http://nginx.org/download/nginx-*.tar.gz)
> >
> > 2.4 解压压缩包:
> >
> > > tar -zxvf nginx.\*
>
> 1. 安装 nginx :
>
>    > 3.1 进入解压后的 nginx 目录:
>    >
>    > > cd nginx.\*
>
> > 3.2 执行命令:
> >
> > > ./configure
> >
> > 3.3 执行 make 命令:
> >
> > > make  
> > > TODO: 这个地方应该会出现问题,上完查解决方案
> >
> > 3.4 执行 make install 命令:
> >
> > > make install
>
> 1. 启动 nginx:
>
>    > 4.1 一般在 usr/local/ 会出现 nginx 目录: /usr/local/nginx/sbin/nginx // 回车
>
>    1. 访问:
>
>       直接ip 访问就可以了

