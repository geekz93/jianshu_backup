## 正则表示法 (regular expression)
用从文件中查找特定字符串的一种表示方法，与通配符不同，**按行处理**
> 不同编码方式会影响正则查找的结果
- LANG=C     時：0 1 2 3 4 ... A B C D ... Z a b c d ...z
- LANG=zh_TW 時：0 1 2 3 4 ... a A b B c C d D ... z Z
使用特殊符号可以在不同编码下保证正则的有效性
![正则表达式-symbol.png](http://upload-images.jianshu.io/upload_images/3022282-87b41a7836c86704.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 符号说明
- `*`表示0个或无数个其前面的字符
- `^`行开头符，`$`行结尾符 

## 基础正则表示练习
使用`grep`工具,在test文件中查找
- 搜寻特定字符串：`grep -n 'the' test`
- 反向选择：`grep -vn 'the' test`
- 不区分大小写：`grep -in 'the' test`
- 使用[]: `grep -n 't[ea]st' test`, []中代表一个字符
- 反向选择: `grep -n '[^g]oo' test` 搜寻oo前不是g的字符串
- 取得没有数字的行: `grep -n '[^0-9]' test`
- 使用特殊符号代替：`grep -n '[^[:digit:]]' test` 加强通用性
- 首列定位: `grep '^the' test` test中第一个词是the的行
- 尾列定位: `grep '\.$' test` 显示末尾是.的行,由于.是特殊符号，因此用\转化为普通字符
- 列出空行: `grep '^$' test`
- 表示任一字符: `grep 'g..d' test` 代替了中间两个字符
- 表示0个或多个重复的字符 `grep 'oo*' test` 至少1个o，最多无数个o
- 读取限定范围内的连续字符 `grep 'go\{2,5\}' test` 以g开头后面有2-5个o的会被显示

## 延伸正则表示
* `grep -e`
- `+` : 重复一次或者n次
- `?` : 0个或1个
- `|` : 用或(or)的方法搜寻
- `()`: 括号中内容作为一组搜寻
- `()+`: 多个重复群组搜寻

![正则表达式-symbol-expand.png](http://upload-images.jianshu.io/upload_images/3022282-422eb27917396008.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 实用工具
**sed:** 取代、刪除、新增、擷取（整行处理）
- 删除：`cat test | sed '2,5d'` 删除2-5行
- 插入：`cat test | sed '2a drink tea' `在第二行下插入字符，i：在之上插入
- 取代(行): `cat test | sed '2,5c NO number2-5' ` 将2-5行删除，并插入No number
- 取代(部分): `sed 's/要被取代的字串/新的字串/g'` 对一行中的内容进行取代，结合其他管线命令使用
- 显示：`cat test | sed -n '2,5p' ` 需要加上-n选项
- 直接修改文档：`sed -i '3d' test` 删除test文档中的第3行

**printf:** 格式化输出 `printf 'format' 'content'`
**awk:** 将一行的内容分成数个栏位，根据分隔符，条件来处理
- 格式: `awk '条件类型1{动作1} 条件类型2{动作2} ...' filename` 
**例子:** `awk '{print $1 "\t" $3}' last.txt`
- $1, $2, $3...为变量，分别储存了1，2，3栏位的内容 $0存储了当前行整行的内容
- 内置变量：NF：每行拥有的总栏位数，NR目前处理的行数，FS分割字符(默认为space)
- 支持运算符:`+ - * /`  逻辑符 `< > <= >= ==`

**档案比对工具：diff cmp patch**
- `diff` 用在ascii纯文字档案的比较
- `cmp` 用来比对非文字档案，以字节为单位比对文件的二进制码(牛x)
- `patch` 与diff配合使用，更新或恢复文档 `diff -Naur oldfile newfile > file.patch`

> test
"Open Source" is a good mechanism to develop programs.
apple is my favorite food.
Football game is not use feet only.
this dress doesn't fit me.
However, this dress is about $ 3183 dollars.^M
GNU is free air not free beer.^M
Her hair is very beauty.^M
I can't finish the test.^M
Oh! The soup taste good.^M
motorcycle is cheap than car.
This window is clear.
the symbol '*' is represented as start.
Oh!     My god!
The gd software is a library for drafting programs.^M
You are the best is mean you are the no. 1.
The world <Happy> is the same with "glad".
I like dog.
google is the best tools for search keyword.
goooooogle yes!
go! go! Let's go.
\# I am VBird
