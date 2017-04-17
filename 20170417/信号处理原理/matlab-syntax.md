- **debug**
	- F12 设置短点
	- F5 开始运行，进入调试
	- F10 单步
	- F11 进入函数
	- shift+F11 跳出函数

1. `begin:[part_length:]:end` 按照`part_length`分割区间，默认值为1
```cpp
>> i=1:0.5:2
i = 1.0000    1.5000    2.0000
``` 
2. `size(data)` 得到`data`的行数，列数,返回两个值 
3. `zeros(r, c)` 初始化r行，c列的零矩阵 
4. `log[n](x)`,以n为底x的对数，n默认为e
5. `for n=0:100  ...  end`, n=0到100这101个数
6. 判断语句：
```
if condition
	statement
end
```
7. floor(A) 数组A中的元素全部向前元整
8. ceil(A) 取最近的整数
9. 定义函数：需要新建一个m文件，m文件的第一行设置返回值，函数名，输入值
```
%两个输入参数，两个输出参数
function [out1, out2]= func_name(in1, in2)
...
```
10. `nargin` number of arguments in, 输入参数的个数
11. `isequal(a, b)` 判断a，b两元素是否相等，相等返回1
12. 转置： a = a'
13. 数组分割：matlab中的索引从1开始的
一维数组：arr(a:b) ,取arr中a-b的索引对应的元素，包括a和b
二维数组：arr2(:,2), 取第二列
