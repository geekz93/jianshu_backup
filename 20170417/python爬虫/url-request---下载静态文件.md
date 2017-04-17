# 流程
1. 添加userAgent，作用是模拟浏览访问，而不是python访问（可以省略）
2. 使用Request方法生成requset，将url和userAgent打包（可以省略）
3. 使用urlopen方法发送requset，并得到response对象
4. 使用response对象的read方法读取内容，为二进制数据流
5. 使用open创建'wb'格式文件，将读取的二进制数据写入文件

# 简单实现
```
import urllib.request as urlreq
page=urlreq.urlopen(req)
binf =page.read()

with open( fname, 'wb') as f:
    f.write(binf)
f.close()
```

# 逐步完善
```
import urllib.request as urlreq
import re

url = input('输入网址：')
fname = input('输入文件名：')
if len(fname)==0:
    fname = re.search('[^/]+$',url).group()

#
userAgent = { 'User-Agent':'Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/53.0.2785.116 Safari/537.36'}
req = urlreq.Request(url, headers=userAgent)
page=urlreq.urlopen(req)
binf =page.read()

with open( fname, 'wb') as f:
    f.write(binf)
f.close()

print('文件已保存在当前文件夹...')
input('按下回车退出...')
```
