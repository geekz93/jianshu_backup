## MP算法原理
-  **信号稀疏分解与MP算法**
**信号稀疏分解的思想是：**将一个信号分解成字典库（dictionary或codebook）中的一些原子的组合，要求使用的**原子个数最少，重构误差最小**。对于一个给定字典，**列出所有可能组合**，可以从中选出满足上述要求的一组，得到最优组合。
但是穷举字典中的所有组合是一个NP难题，对于大的字典库几乎无法实现，因此将要求改为从字典库中寻找一个**原子个数尽可能少，重构误差尽可能小**的次优组合。这样计算复杂度会大大降低，MP算法就是能够实现这种要求的算法之一。

- **MP算法原理**
算法假定输入**信号**与字典库中的**原子**在结构上具有一定的**相关性**，这种相关性**通过**信号与原子库中原子的**内积表示**，即内积越大，表示信号与字典库中的这个原子的相关性越大，因此可以使用这个原子来**近似表示**这个信号。当然这种表示会有误差，将表示误差称为**信号残差**，用原信号减去这个原子，得到残差，再通过计算相关性的方式从字典库中选出一个原子表示这个**残差**。迭代进行上述步骤，随着迭代次数的增加，信号残差将越来越小，当满足停止条件时终止迭代，得到一组原子，及残差，将这组原子进行**线性组合**就能**重构输入信号**。

## 步骤
- **step 1-初始化：**生成/选择字典库 D，并对其中的原子做归一化处理 norm(D)，常用的字典库有：[DCT](https://en.wikipedia.org/wiki/Discrete_cosine_transform)，[Gabor](http://ieeexplore.ieee.org/document/258082/?reload=true) ，初始化信号残差 r = s（s为输入信号）
- **step 2-投影：**将信号残差 r 与 D 中的每个原子 v<sub>i</sub> 做内积 p<sub>i</sub>=s<sup>T</sup>v<sub>i</sub>，记录最大的投影长度 p<sub>max</sub>，和它所对应的原子的索引 i
- **step 3-更新：** 更新残差 r = s - p*v<sub>i</sub>
- **step 4-判断：** 当到达设定的迭代次数，或则残差小于设定的阈值的时候停止，否则继续 step2，step3

## 应用-使用DCT字典重构图片
![reconstruct lena](https://im1.shutterfly.com/ng/services/mediarender/THISLIFE/021009631031/media/122852445820/small/1490488194/enhance)github源码：[matching pursuit](https://github.com/supertab/gcode/tree/mp)

**参考：**
[1] [Matching Pursuits with Time-Frequency Dictionaries](http://ieeexplore.ieee.org/document/258082/)
[2] [Matching pursuit of images](http://ieeexplore.ieee.org/document/529037/)
