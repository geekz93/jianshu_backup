编译的时候加上 `-g` 参数
`g++ -g -o chain single_chain.cpp`
- 进入调试：
```
gdb chain//进入gdb
b main //设置断点为 main 函数
r //执行，在开始调试的时候需要先使用 r 执行
```
- 执行到下一个断点：`c`
- 单步执行：`n`
- 进入函数：`s`
- 退出函数：`finish`
- 显示变量：`p variety`
按回车默认执行上一条命令
