### 知识点
- **非贪婪模式**
默认使用的是**贪婪模式**即得到符合条件的最长字符串，
加问号"?"：(.*?)即开启了**非贪婪模式**得到最短的符合条件的字符串
- **让"."匹配所有字符**
第三个参数设置为`re.S`
- **分组匹配**
  - **groups:** 
**一次匹配得到多个结果:** 得到一个元组，有几个括号对元组中就有几个参数，只显示括号的内容
  - **group:** 显示全部内容
- **显示所有得到的子串:** findall(pattern, string, flag)

![](http://upload-images.jianshu.io/upload_images/3022282-f1b604e5fa573c16.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 应用一
1. 将链接中的最后一个反斜杠后的字符分离，保存为文件名
2. 提取 `www.baidu.com`

待处理字符串：https://www.baidu.com/img/bd_logo1.png
使用`search()`方法，正则表达式使用`[ ^/]+$`(从末尾开始到遇到/就停止）


* 实现
```python
import re
url ='https://www.baidu.com/img/bd_logo1.png'
fname=re.search("[^/]+$",url).group()
print(fname)
baidu = re.search("[^/]+baidu[^/]+",url).group()
print(baidu)
```
