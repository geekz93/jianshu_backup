## os
- 显示目录中的文件：`os.listdir()`
- 切换到指定目录：`os.chdir(path)`
- 创建目录：`os.mkdir(path)`

## os.path
- 得到文件大小：`os.path.getsize(filename)`
- 得到文件后缀：`(filename,extension) = os.path.splitext(tempfilename)`

目录操作：
os.mkdir("file")                   创建目录
复制文件：
shutil.copyfile("oldfile","newfile")       oldfile和newfile都只能是文件
shutil.copy("oldfile","newfile")            oldfile只能是文件夹，newfile可以是文件，也可以是目标目录
复制文件夹：
shutil.copytree("olddir","newdir")        olddir和newdir都只能是目录，且newdir必须不存在
重命名文件（目录）
os.rename("oldname","newname")       文件或目录都是使用这条命令
移动文件（目录）
shutil.move("oldpos","newpos")   
删除文件
os.remove("file")
删除目录
os.rmdir("dir")只能删除空目录
shutil.rmtree("dir")    空目录、有内容的目录都可以删
转换目录
os.chdir("path")   换路径
