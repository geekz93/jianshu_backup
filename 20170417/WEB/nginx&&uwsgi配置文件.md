**nginx configure file**
```
# 需要使用绝对路径：将～替换成/home/youaccout(当前登入的用户)
# the upstream component nginx needs to connect to
upstream django {
    server unix:/home/zooo/uwsgi-set/mysite/mysite.sock; # for a file socket
    # server 127.0.0.1:8001; # for a web port socket (we'll use this first)
}

# configuration of the server
server {
    # the port your site will be served on
    listen      8000;
    # the domain name it will serve for
    server_name localhost; # substitute your machine's IP address or FQDN
    charset     utf-8;

    # max upload size
    client_max_body_size 75M;   # adjust to taste

    # Django media
    location /media  {
        alias ~/temp/uwsgi-set/mysite/media;
        autoindex on;
    }

    location /static {
        alias ~/temp/uwsgi-set/mysite/static;
    }

    # Finally, send all non-media requests to the Django server.
    location / {
        uwsgi_pass  django;
        include     ~/temp/uwsgi-set/mysite/uwsgi_params;
    }
}
```
**mysite_uwsgi.ini**
```
# 需要使用绝对路径：将～替换成/home/youaccout(当前登入的用户)
# mysite_uwsgi.ini file
[uwsgi]

# Django-related settings
# the base directory (full path)
chdir           = ~/temp/uwsgi-set/mysite
# Django's wsgi file
module          = mysite.wsgi
# the virtualenv (full path)
home            = ~/temp/uwsgi-set

# process-related settings
# master
master          = true
# maximum number of worker processes
processes       = 4
# the socket (use the full path to be safe
socket          = ~/temp/uwsgi-set/mysite/mysite.sock
# ... with appropriate permissions - may be needed
chmod-socket    = 666
```
