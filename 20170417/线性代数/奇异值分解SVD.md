# 定义
对A<sub>mxn</sub>进行SVD: 
![A的SVD](http://upload-images.jianshu.io/upload_images/3022282-bb95b75c0fdb7932.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- **记：F=A<sup>T</sup>A**
- **排序：** F的特征值为非负，将它们按照降序排列，它们对应的特征向量排列顺序和特征值一样
- **A的奇异值：** F的非零**特征值**的平方根
- **A的右奇异向量：**V的列向量、F的特征向量（单位化后的特征向量)
- **左奇异向量：**U的列向量（单位化的）
- **R<sup>m</sup>的一组正交基：** **m个**非零向量（如果有0向量，它们就线性相关了），它们**线性无关**，**正交**（两两内积为零）

# SVD步骤
目的：理解3个矩阵的结构，在数值计算中并不是按照下面步骤来的
- **Step1：计算e和v**
A<sup>T</sup>A生成对称矩阵F，计算F的特征值e和特征向量v

- **Step2：生成 Σ<sub>mxn</sub> 和 V<sub>nxn</sub>**
  * 计算奇异值σ，按降序排列，diag(σ)形成对角矩阵，将它放入zeros(size(A))中构成 Σ<sub>mxn</sub>
  * 将特征向量v 归一化，按照特征值的对应顺序排列，构成 V=[v1, v2,...,vn] = V<sub>nxn</sub>，对于应不同e的v有正交关系，对应相同e的v需要进行正交化处理

- **Step3：生成 U<sub>mxm</sub>**
{Av1, Av2，...，Avr} 是ColA的一组正交基，将它们标准化（单位化），即除以对应的σ后，就得到了 一组标准正交基 { u1, u2, ..., ur }，将它扩充成 R<sup>m</sup> 空间的标准正交基｛u1, u2, ..., ur , ..., um}就构成了 U<sub>mxm</sub>

# numpy.linalg中的svd

- 程序

```
import numpy as np
import numpy.linalg as linalg

A = np.arange(27).reshape((3,9))
# U,E,V的顺序与分解公式的顺序对应
# E中只保留了A的奇异值，需要扩充
# 成对角矩阵才能反向验证
U,E,V = linalg.svd(A)
```
- 结果
![svd result](http://upload-images.jianshu.io/upload_images/3022282-8531c7275ab3c06f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
E 中存在很小的值，认为这个值为0

# 推导
![svd公式的推导](http://upload-images.jianshu.io/upload_images/3022282-7672b7267564846e.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
# 原理 （old）
![1830207423.jpg](http://upload-images.jianshu.io/upload_images/3022282-b96617a2206536f5.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
