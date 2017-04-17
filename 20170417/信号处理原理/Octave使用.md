- **[Online IDE](https://www.tutorialspoint.com/execute_matlab_online.php)**

### 在shell中运行m文件
- 先进入`octave`
- 在`octave`中执行`run filepath` 可以使用相对路径

# octave install package
- `pkg install -forge package_name `
课题需要使用的包：image，signal（需要先安装control）

# syntax
- 不等于：~=
- 函数指针：@function
- 显示：
disp(sprintf('2 decimals: %0.2f',a))
2 decimals: 3.14
- format 控制原始输出， format long显示长输出

# 矩阵操作
- 生成矩阵：ones(2,3), zeros(2,3), rand(2,3) 生成全是1，0，随机数的2x3矩阵
单位矩阵I：eye(5)， 高斯分布： randn(1,100)
魔术矩阵：magic(3), 行和列的和都相等
- a = [1 2 2], 为1行3列矩阵
- size(A): 得到A的维度，1个1xn大小的矩阵, length(A)得到最大维度
- ':' ：表示该行或者该列的所有元素
- A = [A, [1;2;3]] : 向矩阵中新放入一列到最后
- A(:): 把A中所有元素放入一个列向量
- 拼接矩阵：A = [B C] and A = [B; C]

## 运算
- 默认按照矩阵法则运算，如果要按照对应元素运算使用"."
- max(A): 显示每列的最大值，find(max(A))：返回最大值对应的索引（1开始）
- floor,ceil: 向下和向下圆整
- sum: 加法（列），prod：乘法(列) 默认为计算列，max(A, [], 2)--改为计算行

- load file.dat 加载file文件， load('featureX.dat', 'price.dat')
- who: 查看系统中储存的变量, whos查看变量的详细信息
- clear price: 清除price变量
- save price.dat price: 将price变量存盘
- save price.txt price -ascii: 以文本的形式保存

## 控制语句
- for循环
```
ind = 1:10;
for i=ind,
  disp(i);
end;
```

- while
```
while i<5,
  i=i+1;
end;
```
- if-elseif-else
```
if v == 1,
  disp('the value is one')
elseif v==2,
  disp('the value is two)
else,
  disp(v)
end;
```

- 定义函数
```
function J = costFunctionJ(X, y, theta)
...
J = X+y*theta
```

- 使用addpath('path')添加搜索路径
- pkg load image # add image package in octave

## 图像
- imshow(im, [])，[]的作用是将浮点型数据映射到[0, 255]，最小值对应0， 最大值对应255
