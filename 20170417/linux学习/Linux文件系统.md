## 1 文件系统分类

## 2 文件系统与目录
* 目录：
当在linux下创建一个目录时，文件系统会分配一个inode与至少一块block给该目录使用
inode: 记录该目录的相关权限与属性，及block号
block: 记录目录中的文件名,如果一个block不够记录文件名，将会分配多个block

* 文件：
分配与文件大小相等的block来存储数据，另外还需要多一个block用来记录block号

* 目录树的读取：
先读取目录的inode信息，根据权限信息(r,w,x)判读是否具有读取该目录block的权限，如果具有权限则读取block,根据block记录的文件名找到对应文件的inode，再根据inode信息读取block

* 新建一个文件时，文件系统的行为
  - 先确定该目录是否具有w与x的权限，若有的话才能新增
  - 根据inode bitmap找到没有使用的inode号码，将新文件的权限写入
  - 根据block bitmap找到没有使用中的block号码，并将实际的数据写入block中，且更新incode的block数据指向
  - 将刚写入的inode与block数据同步更新inode bitmap与block bitmap，并更新superblock 

* 日志式文件系统: 在filesystem中规划出一个区块，专门用于记录文件修订时的步骤
为了避免文件系统不一致的情况发生（在inode和block中有数据而，bitmap中没有记录）产生的
  - 预备：当系统要写入一个文件时，会先在日志记录区中记录某文件准备要写入的信息；
  - 实际写入：开始吸入文件的权限与数据，开始更新metdata的数据；
  - 结束：完成数据与metadata的更新后，在日志记录区块中完成该文件的记录

* 文件系统的运行
编辑文件时系统将文件加载到内存中，未被改动的块计为clean，改动后的块记为dirty，系统会不定时将dirty的数据写回到磁盘中，也可以使用`sync`手动将内中的数据写回到磁盘中

* XFS文件系统(vbird_p362)
* 磁盘与目录的容量
> 磁盘-分区partition-挂载-文件系统
  - `df [-ahikHTm] filename ` 列出文件系统的使用情况,读取的范围主要在Superblock
  > `df -h ` 以更容易读的格式显示
  - `du [-ahsSkm] filename` 列出文件的大小

* Symbolic Link 和 Hard Link
  - `SL` 相当于快捷方式，源文件删除了就无法打开了,创建SL`ln -s sourcefile filename`,链接文件的大小与源文件的文件名有关，test5为5字符，则链接test_sl的大小为5Byte,`sl`相当于创建了一个文件，因此会分配block和inode
  - `HL` 文件名链接到inode，HL的目的是多个文件名链接到同一个inode，这样只要有一个文件还在，都能读取到文件内容，创建HL`ln sourceflie filename`,ln指令默认就是创建HL，创建HL磁盘的inode和空间不会改变，文件属性中的link参数会加1
  > 限制: 1.不能link目录，2.不能跨filesystem
> 由于HL不能link目录，因此SL使用更广，`ln [-sf] 来源文件 目标文件`,f(如果目标文件存在，则先将目标文件移除再创建

> 关于目录中的link数，在目录中创建一个子目录时，该目录的link数会加1，因为该子目录中有 .. 目录
