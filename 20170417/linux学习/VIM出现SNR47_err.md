**问题：**
使用vim打开文件时出现以下错误
![snr47](http://upload-images.jianshu.io/upload_images/3022282-639b0e10a9b5e685.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**解决：**
是由于改变了系统的语言变量导致的
使用locale命令查看，发现LC_ALL没有被设置
使用`export LC_ALL=zh_CN.UTF-8` 解决
