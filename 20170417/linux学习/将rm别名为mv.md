**目的:** 使用rm并不是直接删除文件，而是将其移动到回收站
* 通过函数实现 mv功能：移动到回收站
在`.bashrc`文件中添加：
```
 alias rm=trash                                                               
 trash()                                
 {                                      
     mv $@ ~/.trash/                    
 } 
```
- 显示回收站的内容：`alias lstrash='ll ~/.trash/' `
- 清空回收站：`alias clrtrash='/bin/rm -rf ~/.trash/*'`
