**参考:** [uwsgi document](http://uwsgi-docs.readthedocs.io/en/latest/tutorials/Django_and_nginx.html?highlight=django#virtualenv)，官网上使用的是pip进行安装，比源码安装方便很多（推荐）
> **系统**: ubuntu 12.04  x84_64

## web通信层次结构
     web client <-> web server <-> the socket <-> uwsgi <-> Django
- **web client**：顶层 - 浏览器 - 浏览器显示的页面，用户的操作界面
- **web server**：服务器 - ngnix - 处理静态请求，转发动态请求 - 接收uwsgi的数据
- **the socket**：服务器之间的通信，ngnix通过socket将动态请求传输传输至uwsgi
- **uwsgi**：服务器 - 传送动态请求至Django - 接收Django的数据 - 传送数据至ngnix
- **Django**：底层 - python的web框架
> 对web通信过程的理解：用户在浏览器输入网址`http://www.localhost:8000` 按下回车后浏览器所做的事情就是将页面数据以`http`协议规定的格式发给ngnix，ngnix收到数据后解析，如果是静态请求(如访问图片，视频等文件)就直接将文件包装成http格式返回给浏览器，用户就可以直接看到内容了；如果是动态请求(如刷新验证码)[动态和静态的区别](http://support.exsitewebware.com/cgi/page.cgi/articles.html/Content_Management/Static_vs_Dynamic_Content)，ngnix将请求通过socket发送给uwsgi，uwsgi解析http协议，将数据部分以wsgi协议规定的格式发送给Django；Django解析、处理数据，将处理的结果以wsgi格式发送给uwsgi；uwsgi收到处理结果后通过socket发送至nginx，nginx将结果包装成http格式发送给浏览器完成整个通信

## web服务器组件安装
1. 更系软件源：使用[阿里的镜像](http://mirrors.aliyun.com/help/ubuntu)
```
sudo mv /etc/apt/sources.list /etc/apt/sources.list.back #备份软件源文件
sudo vi /etc/apt/sources.list #添加新浪软件源
sudo apt-get update #更新
```
2. 安装 python3-dev
`sudo apt-get install python3-dev -y`
建立软链接将python链接至python3.4
`sudo cp /usr/bin/python /usr/bin/python.back` 备份之前的python
`sudo ln -s /usr/bin/python3.4 /usr/bin/python` 创建软链

3. 安装 virtualenv（源码）
```
cd ~ && mkdir temp/ && cd temp/ # 在家目录中建立temp/目录，进入temp/目录
wget https://pypi.python.org/packages/source/v/virtualenv/virtualenv-15.0.0.tar.gz # 下载源码，如果版本过低可能不支持python3
tar -zxf virtualenv-15.0.0.tar.gz && cd virtuallenv-15.0.0 #解压,进入目录
sudo python setup.py install # 安装
```
4. 开启virtual环境
```
cd .. #返回temp
virtualenv uwsgi-set
cd uwsgi-set
source bin/activate #启动虚拟环境
```
5. 安装Django（源码）
与安装virtualenv过程一样，[源码下载](https://pypi.python.org/pypi/Django/1.10.3#downloads)，解压进入解压得到的目录
`python setup.py install` 这里由于是在虚拟环境中所以不用使用sudo（在step4 创建的uwsgi-set目录中）
建立Django项目
```
django-admin.py startproject mysite
cd mysite
```
6. 安装uwsgi（源码）
  * [uwsgi源码下载](https://pypi.python.org/packages/11/ef/3d64655693e12f163f659bc3a45837893d7ebbb242e608feb9adc788d2ca/uwsgi-2.0.14.tar.gz)，tar解压，进入目录
```
make #编译
mv uwsgi ~/temp/uwsgi-set/bin/ #将编译好的可执行文件放进虚拟环境的bin目录中
```
  * **测试uwsgi+python**
`vi test.py`
输入：
```
def application(env, start_response): 
    start_response('200 OK', [('Content-Type','text/html')]) 
    return [b"Hello World"]
```
`uwsgi --http :8000 --wsgi-file test.py` 开启uwsgi服务，在浏览器中输入 `127.0.0.1:8000` 显示Hello World说明已经正常安装
  * **测试uwsgi+django**
```
python manage.py runserver 0.0.0.0:8000 #起django
uwsgi --http :8001 --module mysite.wsgi #起uwsgi
```
浏览器中输入 `127.0.0.1:8000` 显示django页面说明已经正常安装

7. 安装nginx
`ctrl+alt+t` 新开启一个terminal，安装nginx
```
sudo apt-get install nginx
sudo /etc/init.d/nginx start
```
**测试**：在浏览器中输入`127.0.0.1`，显示nginx的欢迎界面说明安装正常

## web服务器配置
1. 配置nginx静态目录
  * 建立配置文件
```
cd ~/temp/uwsgi-set/mysite #进入django工程目录mysite
cp /etc/ngnix/uwsgi_params .  #复制uwsgi_params到当前目录
mkdir media/ static/ #创建静态文件存放目录
vi mysite_nginx.conf #建立nginx的配置文件
``` 
[nginx配置文件内容](http://www.jianshu.com/p/0676abe9c691)
 * 创建软链到nginx目录中
`sudo ln -s ~/path/to/your/mysite/mysite_nginx.conf /etc/nginx/sites-enabled/`
  * 部署静态文件
在`mysite/settings.py`中添加`STATIC_ROOT = os.path.join(BASE_DIR, "static/")`，运行`python manage.py collectstatic`
  * 重新开启nginx服务
`sudo /etc/init.d/nginx restart`
  * **测试**：将图片photo.png放入media/目录中，在浏览器中输入`localhost:8000/media/photo.png`能够显示图片就表示静态文件部署成功

2. 配置nginx+uwsgi+django
  * 使用socket通信
将`mysite_nginx.conf`文件中的server下的` server 127.0.0.1:8001;`注释掉`#`,添加`server unix:~/temp/uwsgi-set/mysite/mysite.sock;#替换～为/home/当前登录的用户` **注意:** unix:后面要紧跟路径，之间不能有空格
  * 在mysite目录(父mysite目录)中建立`mysite_uwsgi.ini`文件
[uwsgi配置文件内容](http://www.jianshu.com/p/0676abe9c691)

  * 起uwsgi
`uwsgi --ini mysite_uwsgi.ini`
  * **测试**：在浏览器中输入`localhost:8000`显示的是django的页面说明配置成功～

这样一个nginx+uwsgi+django的web服务器就算搭建完成了～
> 在开启uwsig时报错：`ImportError: No module named 'encodings'` 原因：
1. uwsgi 版本太老不支持python3，一般使用pip安装不会出现这个问题
解决方法：从官网下载最新版本：[下载地址](projects.unbit.it/downloads/)
2. 使用的是默认python2.7 编译的uwsgi，用来跑python3的文件
解决方法：修改安装包中的Makefile文件：PYTHON :=python 改为 PYTHON :=python3 再make
3. ini文件中 home路径设置错误，需要设置为virtualenv的建立的目录，而不是项目目录
`home            = /home/zooo/web-share/mysite  <--错误`
`home            = /home/zooo/web-share/  <--正确`
