# 0 从新建文档开始
新建文档的时候系统初始化所有输入为正文样式，同时系统初始化3个标题样式

![初始样式](http://upload-images.jianshu.io/upload_images/3022282-494022795a73b7a1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

当随着插入页眉页脚，目录，链接等操作，系统将会生成对应的样式
中文和西文分别设置不同的字体，可以让同一种样式下显示不同格式的汉字和英文（数字123tutu也在英文样式的控制中）

![正文样式](http://upload-images.jianshu.io/upload_images/3022282-b642445762582b1e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 1 样式基于 （样式为标题1）
将样式基于那项设置的样式称为父样式
样式基于，就是继承父样式的所有设置，同时可以自己可以改动，或者增加样式

![标题1的样式](http://upload-images.jianshu.io/upload_images/3022282-e6b76153be5a5b4a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这里的标题1继承了正文的字体样式：**宋体（格式下的“+中文正文”就是表示用的是和正文一样的字体）**，但是字体改成了二号，因此有了这个显示效果。看起来标题1只继承了字体样式。
**样式基于的原理**和面向对象编程的**类的继承和派生**一样：正文相当于父类，标题1相当于正文派生的子类

## 1.1 样式基于 （样式为标题2）
标题2的样式与标题1样式的区别是没有继承正文样式的字体，因此改变正文样式的字体，正文和标题1的字体变了，而标题2的字体没有变

![标题2的样式](http://upload-images.jianshu.io/upload_images/3022282-7e62da257291cdde.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![修改正文字体为：幼圆](http://upload-images.jianshu.io/upload_images/3022282-0187566050d821cb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 2 后序段落样式

![后续段落样式](http://upload-images.jianshu.io/upload_images/3022282-6af020a8198b8516.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
后序段落样式就是换行后的输入样式，看下面栗子：观察按下回车后发生了什么？

![按下两次回车](http://upload-images.jianshu.io/upload_images/3022282-154ab5c8cc35fe72.gif?imageMogr2/auto-orient/strip)
答：观察到光标的位置和长度发生了变换，这是因为，按下回车后发生了样式的切换。下面是切换过程：
在动图中，将图片的样式设置为图片本体，在这个样式中设置了后续段落样式为图片标题，因此按下回车后样式切换为图片标题，而在图片标题中设置的后序段落样式为正文，因此第二次按下回车后样式切换为正文样式，正文样式的后续段落样式是它自己，因此不再切换了。

![按两次回车，输入样式的切换](http://upload-images.jianshu.io/upload_images/3022282-ceccd22579599013.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


![新建的两个样式](http://upload-images.jianshu.io/upload_images/3022282-d08932aaac4e6759.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![图片本体样式](http://upload-images.jianshu.io/upload_images/3022282-8c75f42970664203.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![图片标题样式](http://upload-images.jianshu.io/upload_images/3022282-b68ef2105496236a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 3 还有什么...
## 3.1 控制权限
单独修改内容 > 设置的样式 > 父样式，单独修改word的内容是最高级操作，它不受样式的影响
什么是单独修改内容？
就是选中内容再进行修改（我们平时做的最多的操作）

![单独修改：将“内容”设置为新宋体字](http://upload-images.jianshu.io/upload_images/3022282-89144398887af817.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
这样修改后，即使修改了正文样式中的字体，它也不会变，想要改变它只有再次选中它调整字体
## 3.2 对已经乱了的文章修改
设置好正文样式 —— 选中全部内容 —— 应用正文样式 —— 逐个添加样式
