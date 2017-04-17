- `ls` 按照大小S，最后修改时间t排序显示（反序--reverse），列出属性，显示隐藏文件
- `file` 查看文件类型
- `cp -u *.html destination` 将destination中没有的或者发生改动的html文件拷贝到其中, 保留全部属性-a
- `mv` 也有-u 升级移动选项
- **通配符**
*, ? [characters] [!characters] [[:class:]]
![character_class](http://upload-images.jianshu.io/upload_images/3022282-f5854daff12205d7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- `rm` 避免错删文件的方法：先是哟个ls看删除的文件是否正确，再按上键调回刚刚的输入，将ls替换为rm
- `ln` ln file link(建立硬链接) ls -s item link(建立软链接)
**硬链接的限制:** 只能应用于同一分区的文件；不能对文件夹建立链接
**判别硬链接的两文件是否为同一个文件:** `ls -li` -i 选项显示节点号，硬链接的两文件有相同的节点号
**建立软链接可以使用相对路径**

- 查询可执行文件的路径： `which`
无法查询内置函数，如which cd将报错
- 查看文件的**man**和命令的man：`man 5 passwd` `man passwd`
- 查看**简短的指令说明：**`whatis`
- **网页形式的帮助：**`info`  n:next node，p:previous node，u:go to menu，上下移动到超链接，按enter进入超链接
- 建立**别名**&取消别名：`alias` `unalias`
在建立别名前先使用type查看命令名称有没有与系统设定的相冲突

## 6-重定向 >
2 是标准错误流(standard error stream)的文件描述符(file descriptor)
1 标准输出流，
0 标准输入流文件描述符
### 重定向stdout stderr
- 重写文件的重定向：`ls /bin > ls-output.txt`
- 增量重定向：`ls /bin >> ls-output.txt`
- 错误流重定向：`ls /fuck 2> ls-error.txt`
- 重定向标准输出流和错误流：
方法1：`ls -l /bin/usr &> ls-output.txt`
方法2：`ls -l /bin/usr > ls-output.txt 2>&1`

### 重定向stdin
- cat **接收标准输入**，< 是输入符
直接使用cat不加参数，bash将会等待从键盘的输入，当按下ctrl+d时结束，cat将会显示之前的输入。
`cat > file`: 将键盘的输入写到file中
cat 可以**显示非打印字符**如：tab，LFD, M-...
cat 可以**合并文件**， cat file0* file

### 管线命令 “|”
**指令**通过管道命令从stdin接收数据和将数据输出到stdout
- **"|" 与 ">" 的区别**
"|" 作用于指令，">"作用于文件，">"默认会覆盖同名文件
- **sort**
`ls /bin /usr/bin | sort | less`
ls两个目录时，会显示两个列表，使用sort将其合并为一个列表
- **uniq**
与sort一起用，先排序，后过滤同名文件
- **wc(word count)**
默认输出 行数，词数，字节数 这3个参数
- **grep**
"-i" 不区分大小写
"-v" 列出为匹配的
- **head**和**tail**
"-n 5" 列出前5行和后5行
**tail**: "-f" 可以持续输出文件末尾新添加的内容，question：使用文本编辑器在末尾写入内容不更新
- **tee**
每用一个tee就将stdin复制一份，用于写入文件和stdout，可以使用多个tee复制多分stdin

## 7-bash中的扩展与引用

- 显示除去"./和../"外的所有文件：ls -A
- 波浪线扩展 ～：显示当前用户的家目录
cd ~foo #进入foo的家目录
- 算数扩展：$((expression))
- **花括号扩展{}**
echo {01..03} -> 01 02 03
还可以组合应用：
echo a{A{1,2},B{3,4}}b -> aA1b aA2b aB3b aB4b
**批量顺序建立目录**
mkdir {2007..2009}-{01..12}
- **参数扩展**
echo $USER -> zooo
**显示所有参数（变量）：** printenv
- **命令替换（command substitution）**
file $(ls -d /usr/bin/* | grep zip) #先执行阔号内的命令，再将执行结果作为参数传给前一个命令,支持管线， 也可以使用“`(反单引号)”对代替$()

> 加上 -d 只显示目录，在 ls * 的时候不显示目录中的文件

### bash中双引号和单引号
- 双引号""
所有特殊字符都作为普通字符,如：$, \ ，空格也被当成普通字符而不作为指令之间的分隔符,他们单独出现忽略其特殊意义，但是黏在一起出现有时可以输出：
`echo "$ USER" -> $ USER`
`echo "$USER" -> zooo #$USER被执行了`
参数扩展，数学扩展和指令替换（command substitution）可以输出，例如：
`echo "$USER $((2+2)) $(cal)"`

- 单引号''
被单引号包括的所有字符都作为普通字符

- 对比
```
[me@linuxbox ~]$ echo text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER
text /home/me/ls-output.txt a b foo 4 me
[me@linuxbox ~]$ echo "text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER"
text ~/*.txt {a,b} foo 4 me
[me@linuxbox ~]$ echo 'text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER'
text ~/*.txt {a,b} $(echo foo) $((2+2)) $USER
```
## 9-权限管理
- id 查看当前账户的id信息
**uid(user ID):** 当一个创建一个用户时，系统就会分配一个数字，称为用户id
**gid(primary group ID):** 用户加入一个群组时会得到一个数字，成为群id
**文件**
```
/etc/passwd: 存有user (login) name, uid, gid, the account's real name, home directory, and login shell
/etc/group:
/etc/shadow: 存了密码
superuser(uid 0)
```
- 文件权限rwxrwxrwx
- chmod 修改文件权限：只有owner和superuser可以对文件权限进行修改
**方法一：** 每一组rwx->000,开哪个权限对应位置的数置一
`chmod 600 foo.txt` 6->110 因此开的是读和写权限
**方法二：** u->owner g->group o->other
chmod u+x file 为owner添加执行权限
- 指定创建文件的默认权限 umask
umask制定的数字是从默认权限中加上或者减去某项权限,也是对应二进制位的数
原本为创建文件的权限为rw-rw-rw- 666, umash 0001则每次创建文件的权限为rw-rw-r--
- 设置s属性
chmod u+s program: **setuid让程序具有root权利执行?** -rwsr-x-r-x
**setgid:** chmod g+s dir drwxrwsr-x : **新创建的文件与目录所属群组相同**,默认创建文件的组群为用户所在群组
**sticky bit set:** chmod +t dir: drwxrwxrwt 有何作用？

- 切换用户
su -l user: 切换用户，进入该用户的家目录，会新建一个shell
sudo command: 以其root身份执行命令，不会新建shell，配置文件为/etc/sudoers

- 改变文件所有者和用户组
chown [owner][:[group]] file...
改变owner: bob
改变owner，group变为新owner的组: bob:
改变group: :admins
指定owner和group：bob:admins

- 修改密码
passwd [user]

### 10-进程
- 查看进程
ps: 显示当前bash中的进程 x，显示所有进程 (看pid)
top: 动态现实进程
- 后台进程和前台进程
**将程序放在后台运行：** 在后面加上&，xlogo &
**fg %number:** 将后台程序放到前台
**bg %number:** 将前台程序放在后台
**jobs:** 查看当前bash中的进程(看序号)

- 向进程发送信号
**kill [-signal] PID**，也可以使用jobs中的序号代替pid
可以让进程挂起、中断/停止/继续作用相同
**killall [-u user] [-signal] name...** 同时向多个进程发送信号
例子：killall xlogo

### 环境配置
- set: 显示shell和环境变量
- printenv: 仅显示环境变量

login shell 与 non-login shell：需要输入用户名密码进入的shell成为login shell（按ctrl+alt+F1等切换的终端、通过ssh远程登陆的shell等);不需要输入密码打开的shell称为non-login shell(在GUI中打开的shell)

**login shell读取的配置文件：**
/etc/profile：全局配置文件（所有用户都会读取此文件）
~/.bash_profile or ~/.bash_login or ~/.profile（用户自己的配置文件，当前一个不存在时会找后一个文件）
**non-login shell读取的配置文件：**
/etc/bash.bashrc（所有用户的配置文件）
~/.bashrc（个人配置）
**export的作用**
在父bash中export某个变量后， 使子bash也可以使用这个变量

- 修改配置文件
添加路径、增加环境变量：.bash_profile或者.profile
其他修改：.bashrc
使设定生效：
bash在打开的时候会读取.bashrc文件，或者使用source
source .bashrc 使bash重读.bashrc文件

# 14-安装包管理
# Ubuntu软件包管理
## 安装
- 在线安装
apt-get update; apt-get install package_name
- 本地安装，下载了deb格式的数据包
dpkg --install package_file

## 卸载
apt-get remove package_name

## 升级
- 在线
apt-get update; apt-get upgrade
- 本地
dpkg --install package-file

## 列出已经安装的软件
dpkg --list 
- 查看指定软件是否安装
dpkg --status package-name
- **列出与安装软件有关的文件**
dpkg --search file-name

# 15 存储设备
使用的命令：mount umount fdisk fsck mkfs fdformat dd genisoimage wodim md5sum
## 存储设备的名称
软盘：fd×
IDE并口硬盘：hd×
SCSI串口硬盘,移动硬盘：sdx
CD:sr

- 查看系统的动态信息：`tail -f /var/log/syslog`

## 创建文件系统
步骤：1.创建新的分区 2.创建文件系统
- umount 挂载的分区
`sudo umount /dev/sda10`
- 使用分区软件fdisk，修改分区
- 创建文件系统
在格式化系统的时候，是否需要修改分区编号？
创建ext3文件系统：`sudo mkfs -t ext3 /dev/sda10`

- 修复磁盘：`sudo fsck /dev/sda10`
- 操作软盘
格式化：`sudo fdformat /dev/fd0`
创建文件系统：`sudo mkfs -t msdos /dev/fd0`

## 移动数据
- 二进制块移动：`dd` 可以直接拷贝整个磁盘
格式：`dd if=input_file of=output_file [bs=block_size [count=blocks]]`，**危险命令，使用前确认格式，和磁盘名称**

## 创建CD-ROM镜像
- step1 创建iso文件
直接拷贝镜像：`dd if=/dev/cdrom of=ubuntu.iso`
将文件打包成iso：`genisoimage -o cd-rom.iso -R -J ~/cd-rom-files` #cd-rom-files是装文件的目录
- step2 写入iso文件
`wodim dev=/dev/cdrw image.iso`

- 挂载iso文件
```
mkdir /mnt/iso_image
mount -t iso9660 -o loop image.iso /mnt/iso_image
```
- 清除CD上的数据（对于可读写CD)
`wodim dev=/dev/cdrw blank=fast`

## 创建md5
`md5sum image.iso`

# 16-networking

- 网络配置工具：ip
用于代替ifconfig，查看接口：`ip a`

## 传输数据
- ftp 
ftp的用户名和密码是使用明文在网络中传输的，一般的ftp都设置为任何人都能下载，称为anonymous模式，登陆的时候输入用户名anonymous,和任意密码都能登陆，在browser中输入ftp：//就开始从FTP 服务器下载文件
与服务器建立连接: `ftp fileserver`
登陆：用户名：anonymous，密码：任意
设置本地目录：`lcd testdir`
下载文件到这个目录：`get file.iso`
退出：bye
- lftp 与ftp操作类似，比它能强大
- wget 从网页和ftp服务器下载文件

## 远程登陆
- ssh
需要安装OpenSSH-server和client才能实现远程登陆
