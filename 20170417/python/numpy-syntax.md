A为mxn矩阵
- **让索引出的单个元素成为一个矩阵：** `A[np.arange([0])]`
- **转换数据类型：**`A = A.astype(np.float64)`，转为 float64 矩阵
- **矩阵转置：**`A.transpose()或A.T`，返回转置矩阵
- **合并列表：** `np.append(list1, list2)`
- **矩阵乘法：** `np.dot(A,B)` AxB，默认是对应元素相乘
- **扩充：**
a 是n维向量
`np.tile(a,(3,1))`：纵向堆叠，使a堆叠3行
将a，添加到A的第一列： a先使用`reshape(len(a), 1)`处理，将 a 由向量变成 1 维数组
方法1：`np.c_(a, A)`
方法2：`np.concatenate((first, A), axis=1)`

- **计算矩阵元素的和：**
A.sum()：默认是所有元素相加
A.sum(axis=1)：指定横向相加，即列相加
- **return the position of max value返回最大值所在的位置**
`A.argmax(), consider matrix as one line!`默认全部作为 1 维向量，也可以指定方向：`axis=0，1，2，3`
- **数据的方差，标准差**
方差：np.var(A, axis=0),
标准差：np.std(A,axis=0), 指定轴
- **网格函数：**`x2,y2 = numpy.meshgrid(x,y)` 做3d图时用到
假设传入的x为5维行向量，y为10维行向量，meshgrid的作用是将x复制成10行，将y转置后复制成5列，因此返回的x2，y2为10行5列的二维数组
- **向上向下取整：** `np.ceil()/floor()` ceil-天花板，floor-地板

- np.strides: 32位系统值为4？64位系统值为8
