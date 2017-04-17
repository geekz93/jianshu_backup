[编码问题](http://blog.csdn.net/eastmount/article/details/48841593)

# request.js

```
var page = require('webpage').create(),
    system = require('system'),
    address;
address = system.args[1];
 
//init and settings
page.settings.resourceTimeout = 30000 ;
page.settings.XSSAuditingEnabled = true ;
//page.viewportSize = { width: 1000, height: 1000 };
page.settings.userAgent = 'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/37.0.2062.120 Safari/537.36';
page.customHeaders = {
    "Connection" : "keep-alive",
    "Cache-Control" : "max-age=0",
    "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8",
    "Accept-Language": "zh-CN,zh;q=0.8,en;q=0.6",
};
page.open(address, function() {
  console.log(address);
  console.log('begin');
});
//加载页面完毕运行
page.onLoadFinished = function(status) {
  console.log('Status: ' + status);
//在控制台显示页面内容
  console.log(page.content);
  phantom.exit();
};
```
# python script

```
import os
website = 'http://shuju.wdzj.com/problem-1.html'
cmd = './phantomjs'+' request.js'+' '+ website
# python调用系统命令
tmp = os.popen(cmd)
# 得到网页内容，在read的时候可能会出现编码问题，目前未解决
# read()后转为str就是可读的内容
content = str(tmp.read())
```
