bs（browser/ server）架构和cs（client / server） 架构

## 安装集成环境
- **系统**: ubuntu 12.0.4  cpu架构：x86_64
- **安装包**: XAMPP，集成了 Apache + MariaDB + PHP + Perl
官网上下载二进制安装包后，添加x权限，运行安装

## apache体验
在浏览器中输入
- `127.0.0.1:8080`：apache创建的模拟ip
- 本机ip地址：同一个网段中的设备，输入本机ip即可以访问服务器网页
- `localhost:8080`
进入目录dashboard/，进入目录后会根据 httpd.conf文件中的设置寻找相关文件，`index.html index.html.var index.php index.php3 index.php4` 有的话就打开这个文件
```
#
# DirectoryIndex: sets the file that Apache will serve if a directory
# is requested.
#
<IfModule dir_module>
    #DirectoryIndex index.html
    # XAMPP
    DirectoryIndex index.html index.html.var index.php index.php3 index.php4
</IfModule>
```
如果没有找到相关文件，将会直接显示目录

- 默认安装的文件在`/opt/lampp/`目录中
- 主页目录地址为`/opt/lampp/htdocs/dashboard/`
