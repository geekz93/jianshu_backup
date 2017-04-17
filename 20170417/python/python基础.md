- **三元表达式：** `value= true_express if condition else false_ecpress`

- **交换 a,b 变量的值：** `b, a = a, b`

- enumerate(iter): 得到一个序列，其中的元素为（位置，值）组成的对，使用 `for a, b in enumerate(iter)` 从中取值

- **格式化输出：** `temp = '%.2f, %s, %d'; temp%(2.342, 'sf', 2)`

- **函数**
  * `def func(x, y, z=None)`：x, y是位置参数，z是关键字参数
  * `def func(*args, **kw)形`: args是任意个无名参数，在函数中保存为 args 列表的形式，kw 是任意个关键字参数，在函数中保存为 kw 字典的形式。任意函数都可以通过 `func(*args, **kw)` 的形式调用它
> 在外部组合，`arg=[1,2,3], sig={'city':'beijing', 'sex':'man'}`, 使用 `func(*arg, **sig)` 传入

- 变量的传递，是传引用，变量 s，f 传到函数中了，在函数中
```
def add(var_a, var_c):
    result = s + f
    print('result=%d\ns=%d\nf=%d'%(result, s, f))

s, f = 1, 2
7fc8f49ca7760e
add(s, f) # result=3, s=var_a=1, f=var_b=2
```
- 通过`is, is not`判断两变量是否指向同一个对象 
- `isinstance(obj, type)`: 判断对象类型
- 可迭代： 具有 `__iter__` 方法，不可迭代对象使用 iter(obj) 时将报错
- `list` 与`tuple`的区别， `tuple`中的值不可变
- 复数的虚部用 j 表示， `a = 1+2j`, a为复数
- 字符串str中的元素不可变

## 内置函数
- 字符转 ascii 码：`ord('a')`
- ascii 码转字符：`chr(121)`
- 十进制转：八，十六，二进制：`oct(22), hex(22), bin(22)` 记号 `0o26, 0x16, 0b10110'，转十进制：`int('0b10110',2), int(0xfd, 16)`

## 切片（浅拷贝）
list[::2]：从 0 开始步长为 2 正向切片（奇数位置）list[1::2]（偶数位置）
list[::-1]：逆序切片

## 浅拷贝和深拷贝
使用copy.copy()，可以进行对象的浅拷贝，它复制了对象，但对于对象中的元素，依然使用原始的引用.
如果需要复制一个容器对象，以及它里面的所有元素（包含元素的子元素），可以使用copy.deepcopy()进行深拷贝
