- 格式：tar [-xcvp...] -f filename
tar 打包的时候会记录文件的路径，这与filename有关，如果filename包含的是相对路径`./`或者`../`则在tar包中的文件也是相对路径；如果是绝对路径`/home/zooo/test`则包中的文件也是绝对路径，不过在默认情况下tar会将根目录符号去除，防止文件被覆盖即包中文件的路径为`home/zooo/test/file`，因此解压的时候会在`-C`指定的目录或当前目录下出现  `home/zooo/test`三层目录

### 1 基本用法
- 将foo和bar文件打包成archive.tar
           tar -cf archive.tar foo bar 

- 列出archive.tar中的内容
           tar -tvf archive.tar

练习：使用管线指令列出顶层目录

- 解压 archive.tar 到当前目录，后面加 `-C PATH` 解压到指定目录
           tar -xf archive.tar
           tar -xf archive.tar -C directory

### 2 不打包指定文件
     tar -cf test.tar --exclude=./not_include_me* ./*
- **-cf:** 创建包文件
- **--exclude=./not_include_me*:** 不打包当前目录中的`not_include_me`目录（包括该目录和目录中的文件）如果写成 `./not_include_me/*` 则只是不打包该目录中的文件，`not_include_me`目录还是会被打包进来。**bug:** 使用`~/not_include_me*`时exclude失效。在备份的时候要保留全路径就只能使用`--exclude=/home/zooo/test/not_include_me*` 这样才能将这个目录排除打包
- **./*:** 打包当前目录的所有内容，如果要保存文件的全路径，这项也使用绝对路径
