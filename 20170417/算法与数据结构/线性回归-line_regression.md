## 1 什么是线性回归
线性回归属于监督学习的一种（测试样本自带标签），通过对样本的学习，得到拟合函数，根据拟合函数可以对后来的样本进行预测，即输入样本的标签未知，通过拟合函数求出它的标签。

## 2 怎么得到拟合函数（Hypothesis Function）
- **选择拟合函数**
在进行训练之前需要先根据样本的分布特征，选择合适的拟合函数模型，再训练样本得到拟合函数。**一些拟合函数：**
![hypothesis1](http://upload-images.jianshu.io/upload_images/3022282-51b82f512bb46db7.png)
![hypothesis1](http://upload-images.jianshu.io/upload_images/3022282-0fef58cfaa6b0089.png)
![hypothesis1](http://upload-images.jianshu.io/upload_images/3022282-6b171bedc0d332bf.png)
**多项式回归（Polynomial Regression）**，本质就是**多元回归**，原样本只有一个特征 x，采用 x<sup>2</sup> 相当于人为创建了一个新的特征。因此拟合函数可以统一写成：
![multi_feature](http://upload-images.jianshu.io/upload_images/3022282-8164250b75199851.png)
其中的每一个 x 都是样本的一个特征。用向量的形式来表示：
![vectorlize](http://upload-images.jianshu.io/upload_images/3022282-8c5d37d9b479ce78.png)

- **确定 θ**
**原理**是一个很自然的想法，使**拟合总偏差**最小。
为此先确定一组 θ，将每个训练样本带入拟合函数计算出它们对应的标签，这个计算标签可能与它们自身带的标签不同，计算二者的**偏差**，将所有偏差相加，就得到了**拟合总偏差**。通过**梯度下降法**调整 θ，再进行拟合，当找到一组 θ，使得拟合总偏差最小，就将这组 θ 作为确定的 θ。用函数描述如下：(上标表示样本，下标表示样本的特征，这里是使用向量的形式表示了，因此没有下标）
![cost_function.png](http://upload-images.jianshu.io/upload_images/3022282-e561258a7e20ebe8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
这个函数称为**代价函数（cost function）**，确定 θ 的过程就是 **minimize J(θ)** 的过程。

### 2.1 梯度下降法（Gradiant Descent）
对 θ 求偏导，选择一条下降最快的线路，α 为学习速率
![theta j ](http://upload-images.jianshu.io/upload_images/3022282-8b1671b50346c219.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
对求和函数求偏导的过程
![partial derivative](http://upload-images.jianshu.io/upload_images/3022282-ce19139682f49f11.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
每次梯度下降都得到一组 θ，当 θ 的变化很小的时候，算法收敛
- **规范化数据（normlization feature）**
在使用梯度下降法的时候如果特征的取值范围过大，将导致收敛缓慢，因此需要使用规范化函数对每个数据点进行处理，使数据处于一个较小的范围内：
![norm_function1](http://upload-images.jianshu.io/upload_images/3022282-cfec2a9c6875b88f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
avg 为特征 j 的平均值，std 为标准差，还可以选择其他的 norm function 来规范化数据
- **学习数据 α 的选择**
如果 α 过小，则算法收敛很慢，如果 α 过大，将会出现震荡，导致不收敛。在选择 α 的时候先使用 0.001, 0.01, 0.1进行试验，先确定一个范围，然后再慢慢扩大

### 2.2 标准方程（Normal Equation）
- 对于一元方程，`y(t) = a*t + b*t^2 + c`通过对 t 求导： `dy(t)/dt=0` 可以得到使 y(t) 取得最小值的时候的 t。对于多元函数，通过求每个变量的偏导，解方差组可求。因此 minimize J(θ) 可以通过方程的方式来实现： **θ = (X<sup>T</sup>X)<sup>-1</sup>X<sup>T</sup>y**
其中 X 为样本特征构成的矩阵(同一特征在一列上），y 为样本标签组成的列向量
- 使用通用方程不需要设定学习速率和对数据规范化
- **注意：**(X<sup>T</sup>X)<sup>-1</sup>可能会出现不可逆的情况：
    1. X中存在冗余向量 x<sub>i</sub>=kx<sub>j</sub>( i 不等于 j）
    2. 输入样本过少，而每个样本的特征太多

### 2.3 梯度下降法和通用方程的比较
**梯度下降法**，需要进行特征的规范化，需要设置学习速率，算法更复杂，但是时间复杂度低，**适用于样本较大的情况**
**标准方程法**，精确，简便，但是矩阵求的时间复杂度为 O(n<sup>3</sup>)，很高，因此只适用于**小规模样本** 1000 以下
