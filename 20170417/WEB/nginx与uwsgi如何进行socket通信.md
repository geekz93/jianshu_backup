1. 需要有uwsgi_params模块
这个模块在目录`/etc/nginx/`中，将它拷贝到项目目录中，再在mysite_nginx_conf文件的 location /{} 中导入
2. ngnix的配置
在 mysite_nginx_conf 文件中设置socket通信的端口或者文件
```
upstream django{
  server unix:/home/pi/py3env/mysite/mysite.sock; #以文件的形式通信
  # server 127.0.0.1:8001; 以port端口的方式进行socket通信
}
```
3. uwsgi的配置
在uwsgi_ini文件中设置socket路径
`socket =  /home/pi/py3env/mysite/mysite.sock`
修改sock文件属性，使得uwsgi可以读写 socket文件
`chmod-socket = 666`
