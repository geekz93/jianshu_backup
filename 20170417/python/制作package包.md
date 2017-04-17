package 的作用是将 *.py文件放在一个文件夹中方便调用制作 package包：
![](https://note.wiz.cn/api/document/files/unzip/e67f668c-b24a-4b50-8d2e-84c344e96f36/efcc37fc-6fcd-4931-920d-c116f882a21f.3212/index_files/48959b1a-0da8-42de-87ae-57751cfea0ad.png)

导入包中的模块
`>>> import accountTool.vote as vt`
accountTool是一个包，vote是包中的模块

**注意：**
将单个的py文件作为模块导入其他py中，python会在当前目录新建一个 `__pycache__/ `目录，其中存放了被导入的py的字节块文件，当其他py再次调用这个py时，python会将`__pycache__/ `目录的编译好的字节块文件直接导入。如果被导入的py文件发生了改动，则需要将`__pycache__ `中的对于字节块文件删除。不然python无法读取py模块的改动
