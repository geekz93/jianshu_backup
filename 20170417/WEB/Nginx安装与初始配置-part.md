## 编译安装的依赖库的依赖库
安装gcc g++的依赖库: build-essential，libtool
pcre依赖库：libpcre3，libpcre3-dev
zlib依赖库：zliblg-dev
ssl依赖库：openssl

## 有关路径
- `/etc/init.d/nginx` -- shell script nginx启动停止控制脚本
- `/etc/default/nginx` -- 文本文件
- `/usr/sbin/nginx` -- 二进制可执行文件，移除后无法通过 init.d/nginx 启动服务

## nginx uwsgi python之间的关系
1. nginx 是对外的服务接口，外部浏览器通过url访问nginx
nginx 接收到浏览器发送过来的http请求，将包进行解析，分析url
2.http为静态文件请求
直接访问用户给nginx配置的静态文件目录，直接返回用户请求的静态文件。
3.http为动态请求
nginx就将请求转发给uwsgi,uwsgi 接收到请求之后将包进行处理，处理成wsgi可以接受的格式，并发给wsgi,wsgi 根据请求调用应用程序的某个文件，某个文件的某个函数，最后处理完将返回值再次交给wsgi,wsgi将返回值进行打包，打包成uwsgi能够接收的格式，uwsgi接收wsgi 发送的请求，并转发给nginx,nginx最终将返回值返回给浏览器
> nginx不是必须的，uwsgi可以完成和浏览器的交互。使用nginx的原因有下几点：
1.安全性：程序不能直接被浏览器访问到，而是通过nginx的接口，在nginx上加上安全性的限制可以达到保护程序的作用
2.负载均衡：nginx的负载均衡能力强
3.静态文件问题：静态文件的访问完全不经过uwsgi及以后的东西，减轻了uwsgi的压力，nginx和uwdgi一个处理静态请求，一个处理动态请求分工细化


## 安装niginx及初始配置
- **平台**: ubuntu 12.04 x86_64
- `sudo apt-get install nginx` 软件源：`http://ubuntu.grn.cat/ubuntu`
**启动nginx**
- `sudo /etc/init.d/nginx start`
**配置文件**
- [配置文件参考](http://www.ha97.com/5194.html)
- **path**: `/etc/nginx/nginx.conf`
`nginx.conf`文件已经将server配置放在了其他文件中，在http{...}中可以找到它的位置：
```
##
# Virtual Host Configs
##
include /etc/nginx/conf.d/*.conf;
include /etc/nginx/sites-enabled/*;
```
在sites-enabled目录中找到一个default文件，它是链接到`site-available/default`文件的，server的配置就在这个文件中
- **修改监听端口** 
`vi /etc/nginx/sites-available/default` 将listen 80 改为listen 8088,修改后在浏览器中输入`127.0.0.1：8088`就能显示nginx网页了

**网页文件**
- **path**: `/usr/share/nginx/www/`
使用127.0.0.1和localhost，ipv4地址看到的index不同(对index.html文件修改后只有127.0.0.1能看到)，但是能够访问目录中的内容(将端口改为默认则显示正常,原因可能是ipv4端口#$%,还是不改端口吧) 下级目录中需要有index文件，否则将会显示403错误（直接访问目录会显示403）
