# 文件的类型与权限
## 使用  ls -l  看到的内容
![文件的十个字符属性](http://upload-images.jianshu.io/upload_images/3022282-be7cfae46b06f8ad.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
### 第一个字符：文件类型
  * d：目录
  * -：文件
  * l：链接文件
  * b：设备文件里的可随机存取设备
  * c：一次性读取设备，如键盘、鼠标

### 接下来的字符中三个一组 rwx：用户的权限 
> 三个用户分别为：`users` `group` `other`

  * r：读（查看文档或者目录的内容），对应数字 4
  * w：写（对文档：编辑文档的内容，对目录：向目录中添加、删除文件），对应数字 2
  * x：执行（对文档：运行文档，对目录：进入目录），对应数字 1

> 例如：-rwxr-xr-- 文档权限的数字表示为 754

## 修改文件属性
* 改变文件所属群组：**chgrp** [-R(递归)] group dir/filename
> 例如：chgrp zooo test

* 改变文件拥有者 **chown**
  * `chown [-R] user dir/filename`只改变拥有者
  * `chown [-R] user:group dir/filename` 同时改变拥有者和群组
  * `chown [-R] .group dir/filename` 改变群组

* 改变文件权限 ** chmod **
  - `chmod 777 test` // test的权限变更为 rwxrwxrwx
  - `chmod o-x;g=w test` // test的group用户设置w权限，others用户减少x权限

## 设置默认权限
- 默认权限
        文件：默认没有执行权限x，最大分值为666
        目录：默认为所有权限都开放，最大分值为777
制定默认权限 `umask`(默认值需要减掉的权限)：默认umask的值为`0022`,关注后3位数(注意：不是数字的减法运算，如umask=003,意思是除去wx权限，而不是666-003=663),设置默认权限在umask后面接数字：umash 002,普通用户只能做临时修改，root用户可以作永久修改
        对于文件的默认权限为644(-rw-r–r–)
        目录的默认权限为755(drwx-r-x-r-x)

## 设置隐藏属性
在`Ext2/3/4`文件系统下，使用 `chattr` 设置隐藏属性(不可修改),使用 `lsattr` 查看
- 设置隐藏属性 `chattr [+-=][ASacdistu] file` 符号 `+,-` 增加或减少一个参数，其他原本存在的不改动，`=` 设置后原有参数被覆盖
        A 若有存取此文件或目录是，atime不会被修改
        S 一般文件是非同步写入磁盘(需要使用sync写磁盘)，设置此参数后对文件进行了任何修改会同步写入磁盘
        a 文件只能增加数据，不能删除也不能修改数据(重要)
        c 压缩文件…
        d dump被执行时，带有d属性的文件不会被dump备份
        i 让一个文件不能被删除/改名/也无法写入或新增数据(root也不能删除它，对系统的安全和有帮助)
        s 文件被删除将完全被移除这个磁盘空间，误删无法恢复
        u 文件被删除了，内容还存在磁盘中
栗子：将 note.txt 设置为 a 属性，只能通过追加的方式增加内容
      设置：sudo chattr +i note.txt
      增加文件内容：echo "hello world" >> note.txt

CentOS7.x使用xfs作为默认文件系统，支持部分chattr参数，xfs文件系统只支持AadiS参数

## 文件的特殊权限
        Set UID s标志出现在拥有者权限上-rwsr-xr-x被成为Set UID，简称SUID(仅对二进制程序有效)
            例子：文件/etc/shadow 记录了登录密码，只有root可以写入，但是普通用户可以通过/usr/bin/passwd修改自己的密码，是通过SUID实现的
        zooo对于passwd具有x权限，passwd的拥有者是root这个帐号
        zooo在执行passwd的过程中，会“暂时”获得root的权限
        /etc/shadow就可以被zooo所执行的passwd修改
        Set GID s出现在群组的x位置 drwx-r-sr-x,简称SGID
            对二进制程序和目录有用(常用在目录上)
        对目录进行设置后，使用者在此目录的有效群组会变成该目录的群组
        使用者在该目录创建的文件与该目录处于同一群组
        Sticky Bit,SBIT,只针对目录有效
                作用：当使用者在该目录下创建文件或目录是，仅有自己与root才有权利删除该文件(不能修改其他用户创建的文件)
        例子：当甲这个使用者于A目录是具有群组或其他人的身份,并且拥有该目录w的权限, 这表示“甲使用者对该目录内任何人创建的目录或文件均可进行 "删除/更名/搬移"等动作。”不过,如果将A目录加上了SBIT的权限项目时,则甲只能够针对自己创建的文件或目录进行删除/更名/移动等动作,而无法删除他人的文件
    设置文件的特殊权限
        SUID:4, SGID:2, SBIT:1 ->在原来的三组权限前增加一组权限

            例：对目录~/Docments/test/设置SUID: chmod 4755 ~/Docments/test/

        字符的方式:SUID: u+s, GUID: g+s, SBIT: o+t

            出现大写的S，T:由于文件所有者本身就没有x权限，因此S，T表示空权限
