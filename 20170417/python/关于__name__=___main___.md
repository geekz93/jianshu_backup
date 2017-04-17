在主函数中 `__name__ 等于 __main__`
如果是导入的模块 __name__ 等于 函数名
```
>>> __name__
'__main__'
>>> import os
>>> os.__name__
'os'
```
使用 `if __name__ == "__main__"：`可以使在导入模块时不让模块中的函数执行
