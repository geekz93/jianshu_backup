- rename支持perl语法的正则表达式 [参考](http://www.tutorialspoint.com/perl/perl_regular_expression.htm)

## rename的使用
**在rename前先使用-n参数测试，看rename结果是否符合预期**
- 对多文件，添加，去除指定内容
![file](http://upload-images.jianshu.io/upload_images/3022282-dd8685460713423b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  * 在文件后面添加`.txt`扩展名
先使用 -n 测试重命名结果，没问题了就直接rename
```
rename -n s/$/\.txt/ *
rename s/$/\.txt/ *
```
![file.txt](http://upload-images.jianshu.io/upload_images/3022282-5170f8c9b6f62366.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  * 去除`.txt`后缀
`rename s/\.txt$// *`
  * 在前面添加2016
`rename s/^/2016/ *`
- 大小写转换
`rename tr/[a-z]/[A-Z]`
与`s///`模式的对比
![compare2s.png](http://upload-images.jianshu.io/upload_images/3022282-ea68a91ee19e90bb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 练习
- 指定文件重命名
file1-file3已经添加了2016，现在要在file4前添加2017_而不改变file1-3
![](http://upload-images.jianshu.io/upload_images/3022282-5d50e39122be4c3e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)仅仅用rename不能完成，通过ls，grep一起实现
`ls | grep "^[2]" | rename s/^/2017_/`
> ls列出目录中的所有文件，通过管道传到grep中，grep对每行进行处理，去除开头为2的文件，将过滤后的数据通过管道传给rename改变文件名
