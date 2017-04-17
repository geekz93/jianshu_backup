## bash介绍 
- bash(Bourne Again Shell) is the promote of Bourne Shell
- 合法的shell要写入`/etc/shells`档案？
- shell 记录的历史执行指令保存在家目录的`.bash_history`文档中，里面记录的是前一次登入所下达过的指令，而目前登录所下达的指令被缓存在内存中

## 快捷键
> bash 默认为 `emacs`输入方式，可以通过 `set -o vi` 切换为vi的输入模式
**[参考博客](https://www.oschina.net/question/12_31737)**

### 移动
- 移到行首,行尾：ctrl-a, ctrl-e
- 前,后移动一个单词：alt-f, alt-b
- 前,后移动一个字符：ctrl-f, ctrl-b

### 删除
- 从光标到行首,行尾：ctrl-u, ctrl-k
- 向前删除到空格：ctrl-w
- 光标前,后单词：alt-backspace, alt-d
- 删除当前字符：ctrl-d

### 其它
- 清屏幕：ctrl-l
- 使用上条命令的最后一个参数：alt-.

### 使用history
- 重复上条命令：!!
- history配合grep使用，根据关键字查找使用过的命令
- 执行history列表中的一条命令：!number
- 根据关键字查询：ctrl-r，回车直接执行
- 重复本次命令，执行后不清空：ctrl-o


## shell的常用功能
- 上下键查询历史指令
- tab补全命令，档案
- `alias`设定命令别名
- job control, foreground, background
- shell scripts
- `type [-tpa] name`查询是否为内建指令
- \ 跳脱 \ 后的一个字符，如：`\[enter]`跳脱回车，可以到下一行输入
- 支持通配符
![通配符.png](http://upload-images.jianshu.io/upload_images/3022282-cd7234dd0ae18175.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) ![通配符_prac.png](http://upload-images.jianshu.io/upload_images/3022282-28218c7a4e6db0cc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## 符号
- ' : '内的符号为纯文字
- " : "内的符号可以有属性 "asf $a sd", 会显示变量a的内容
- \` : `内的内容被先执行
- 特殊符号
![bash特殊字符.png](http://upload-images.jianshu.io/upload_images/3022282-5b920493cb5edd8c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

## shell的变量
- 环境变量：影响bash环境操作的变量，通常以大写字符表示如：PATH
- 定义变量：赋值操作`a=/var/spool`, 使用变量在变量名前加`$`
- 使用`echo $variable`来读取variable的内容
- 变量设定规则
    1. 使用=来连接，等号两边不能加空格
    2. 如果要存有空格字符串，可以使用引号将等号右边的变为纯文字
    3. 使用`$(cmd)`将指令运行结果存入变量：`version=$(uname -r)`
    4. `PATH="$PATH":/home/bin`或`PATH=${PATH}:/home/bin`将:/home/bin加入变量
    5. `unset ver`或者`unalias ver`取消ver变量
    6. 使用`\`跳脱特殊符号
- 反引号中的内容会先执行，执行的结果作为外部的输入（反引号1左边的符号）
- 使用`env`观察环境变量
- 使用`set`观察设置的变量, 各变量的含义（man bash然后搜索对应字符，查看详细内容）
    1. `PS1` 设置提示字符，即程序结束后在终端上显示的信息，在 .bashrc, /etc/profile，.profile中
    2. `$` 保存shell的pid
    3. `?` 上一个指令的返回值，0为正常，其他值为错误代码，可以根据这个代码来查询错误的原因 
    4. `OSTYPE, HOSTTYPE, MACHTYPE` 存储硬件,核心等级（如：i386,i686,x86_64）
- 在主程序中使用`export var` 让var可以在子程序中使用
> 默认第一个打开的bash为父程序，在这个bash中再使用bash打开的shell为子程序

- 接收用户输入参数 `read`
- 将变量声明为整形，数组，常量 `declare`
- 定义数组(bash提供一维数组的定义) var[1]="asdf as"
- 限制用户的使用资源 `ulimit`

## 变量内容的修改
- 增加变量内容
a=123
a=000${a} 将000放在123前面了
a=${a}'ccc' 将ccc放在123后了
- 删除变量内容（部分删除）
`${variable#/*sth}` 从前头开始向右删除，支持通配符 `#` 删除短的部分， `##`删除长的部分; `%` 从后向前删除
> 删除的是`#`或`%`后的内容，有长短顺序之分

- 取代变量内容
`${variable/old string/new string}`:取代一处
`${variable//old string/new string}`:取代全部
- 判断变量内容
判定变量是否已经赋值，然后决定是否给该变量赋值
${var-string}:对var未设定有效，${var:-string}:对var为空串或未设定有效

## 变量别名与历史指令
- 查看已有的变量名，直接输入`alias`
- 取消变量别名，`unalias`
- 历史指令`history`,显示下达过的指令
保存在`~/.bash_history`中，最大存量由`HISTSIZE`变量确定,与`!`配合重复上次操作
    - `!number` 重复number号的指令
    - `!!` 重复上次的指令
    - `!al` 重复最近执行的以al开头的指令串
- 指令的搜寻顺序,使用`type -a `查看 
- 在tty欢迎界面显示时间/系统版本/硬件等级，等信息`/etc/issue`,`isssue`文件
    - 远程tty使用的是`/etc/issue.net`文件
- 登录后显示的信息`/etc/motd`,`motd`文件中

## bash的环境配置文件
- bash 的設定檔主要分為 login shell 與 non-login shell。login shell 主要讀取 /etc/profile 與 ~/.bash_profile， non-login shell 則僅讀取 ~/.bashrc
- 在`~/.bashrc`中设置bash的环境，再使用`source`读取设置好的值，source .bashrc文件后原来`.bashrc`文件中的变量别名还会继续保存
- 设置终端机按键 `stty`

## 资料流向重引导
- 重引导输入输出与错误输出流
    - **stdin：< <<(累加) 代号0**
    使用文件的内容代替键盘输入的内容：<
    设置输入的结束字符：<<
    **栗子:** `cat > file <<"eof"` 从键盘输入信息到文件，当输入eof时结束
    - **stdout：> >>(累加) 代号1, stderr: 2> 2>>(累加) 代号2**
    例子：find /home file > list_right 2> list_error 保存正确输出与错误输出到文件
    - 写到同一个文件 `&l`代替文件名
    - 将错误输出丢如黑洞文件`/dev/null`
- 指令执行的判断依据
    `;` 顺序执行，前次结果不会影响下次的执行
    `&&` 前次返回值为1执行，为0则不执行
    `||` 前次返回值为0执行，为1则不执行
    **栗子：** ls ./mhome && echo "exist" || echo "not exist" 如果目录存在输出exist，如果不存在输出not exist

## 管线命令
符号 `|` 管线命令接收的是前一个指令的处理结果`stdout`(对`stderr`不能处理)，常用的管线命令：
- `cut` 按照指定切除行的部分内容，然后显示该行 
- `grep` 根据关键字取出某行
- `sort` 按字符，数字，指定开始位置排序
- `uniq` 重复的行只显示一个，与sort配合使用
- `wc` 显示文件有多少行 字 字符
- `tee` 双重引导，同时将信息保存到文件和输出屏幕(stdout)
栗子：`ls -l /home | tee ~/homefile | more`
- **文字处理**
    - `tr` -d 删除内容，'old' 'new' 替换old为new
    - `col` 将tab转换为对等的空格`-x`；将man文档转化为纯文字`-b`
    - `join` 将有关文件整合在一起，应先用sort排序
    - `paste` 将文件中同一行的内容放在一行,默认以tab分割
    - `expand` 将tab转换为空格，`-t`指定空格数
- `split` 分割命令，-b按设置的大小分割，-l按行分割
    - 分割后文件名为faa，fab，使用 `cat faa fab >> file`合并回原文件
- `xargs` 将前面指令的结果作为参数传给它后面接的指令，与一些不是管道命令的配合使用（实用）
- `-` 的作用，用于代替stdin和stdout
