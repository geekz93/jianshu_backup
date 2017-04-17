观察了样本的多个特征，通过PCA可以分析哪些特征是有用特征

## 名词定义
- **观测矩阵：**设观察了N个样本，将对每个样本观测到的m个特征作为列，N列一起组成观测矩阵S<sub>mxn</sub>，每列称为**观测向量X<sub>i</sub>**
- **样本均值M：**将N个观测向量相加，再除N
- **平均偏差形式（mean-deviation form）：**每个样本向量减去M，组成的矩阵 B，称为具有平均偏差形式的矩阵，它各的样本均值为0
- **协方差矩阵：**S=BB<sup>T</sup>/N-1
- **方差：** 用 x<sub>i</sub> 表示样本 X 的第 i 个特征的集合，协方差矩阵S的对角线上元素 s<sub>jj</sub> 称为 x<sub>j</sub> 的**方差**，它表示 X 的第 j 个特征取值的离散程度 
- **协方差：** S 对角线两边的元素 s<sub>ij</sub> 表示 x<sub>i</sub> 和 s<sub>j</sub> 的相关性
- **全变差：** （迹）S 对角线元素之和

## 主成份分析
- 推导：《线性代数及其应用》p432
协方差矩阵 S 的特征向量称为观测矩阵中数据的主成分，S 最大特征值对应的特征向量称为第一主成份，第二大特征值对应的特征向量称为第二主成分
- PCA确定了一个变量替换 Y<sub>k</sub> = P<sup>T</sup>X
P = [u1, u2, ... ] u为主成份，变换的意义在于可以看出 S 中特征的重要程度，特征值越大，说明该特征越重要，如果该特征对应的特征值很小，说明它可以被忽略？
变量替换，求得u后，使用 y=u<sub>T</sub>x 用y代替x（x为具有平均偏差形式的矩阵B中的行向量）**对于PCA一个重要步骤就是解释 y 的作用**
## 计算
使用计算奇异值来代替特征值的计算（计算奇异值，比计算特征值快很多）
协方差矩阵：S = BB<sub>T</sub>/N-1
构造 A = （1/sqrt(N-1)*B<sup>T</sup>，则 S = A<sub>T</sub>A，计算 A 的奇异值σ，它们的平方就是 S 的特征值，

## 程序
```
import numpy as np
import numpy.linalg as linalg

def zpca(A):
    N = A.shape[1]
    # norm A
    M = A.sum(1)/N
    B = A - np.tile(M, (N, 1)).T
    # construct F
    F = B.T / np.sqrt(N-1)
    # covariance matrix
    S = np.dot(F.T, F)
    # SVD F
    U, E, V = linalg.svd(F)
    # eigenvalue of S
    E = E**2
    # eigenvector of S
    V = V.T
    return U, E, V

if __name__ == '__main__':
    # sample matrix
    A = np.array([[120, 125, 125, 135, 145],
                  [61, 60, 64, 68, 72]])
    U, E, V = zpca(A)
    print('U:', U)
    print('E:', E)
    print('V:', V)
```
**运行结果**
![PCA](http://upload-images.jianshu.io/upload_images/3022282-ea71890d17d6b7da.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
