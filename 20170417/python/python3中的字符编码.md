## 1 关于python3的字符串
- python3中的字符串是一个xx对象的实例，当需要以二进制的形式写入文件中时，需要使用 `encode()` 进行编码，编码得到的是以字节为单位的字节流。

![encode](http://upload-images.jianshu.io/upload_images/3022282-bec04b2b939d72f3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

经过编码后，就能以二进制的形式写入文件中

![wb](http://upload-images.jianshu.io/upload_images/3022282-1c4968af482835c2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 与python2.x 中的字符串对比，python2中的字符串直接就是字节流了，因此可以直接将其以二进制的形式写入文件中，**python2中文编码问题，在开头加上：# coding=utf-8**

![py2 wb](http://upload-images.jianshu.io/upload_images/3022282-8c9f75066e51669c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- **应用：** 在调用 c 的动态链接库（linux中为 .so 后缀）中，想把字符串从 python 中传入 .so 要求字符串是字节流的形式，因此使用 python2 可以直接将字符串作为参数传入，而 python3 需要先进行 encode 再传入
> gcc 编译 c 文件成动态链接库：

## 2 关于字符串编码 - utf8
- utf8 是可变长度编码， 中文使用3个字节表示，数字和字母使用  1 字节表示

![utf8](http://upload-images.jianshu.io/upload_images/3022282-10d74ff8a6fec126.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
