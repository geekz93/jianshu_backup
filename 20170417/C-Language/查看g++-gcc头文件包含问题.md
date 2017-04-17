- linux头文件包含在`/usr/include`中
- 查看默认搜索路径`echo $(g++ -v -x c++ -E -)`//会卡住，使用了`-`的原因
```
#include "..." search starts here:
#include <...> search starts here:
下方的路径即默认搜索路径
```

- 添加搜索路径（无作用）
```
CPLUS_INCLUDE_PATH='/new/include/dir'
export CPLUS_INCLUDE_PATH
```
