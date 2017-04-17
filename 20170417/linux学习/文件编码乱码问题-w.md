### 中文乱码原因
- 系统中没有安装相应的字符编码集
如何设置系统编码集？
- 程序中没有导入中文编码

### 文本转码
#### 常见的中文编码集：
- GB2312：国家简体中文字符集，兼容ASCII
- BIG5：统一繁体字编码
- GBK：它是GB2312的扩展，加入对繁体字的支持，兼容GB2312
- GB18030：它解决了中文、日文、朝鲜语等的编码，兼容GBK
- UNICODE：为世界650种语言进行统一编码，UNICODE字符集有多个编码方式，分别是UTF-8，UTF-16和UTF-32

#### 将中文编码集转换为utf-8
- iconv -f source_encoding -t new_encoding > file
- 使用python脚本，文件读写 decode,encode

