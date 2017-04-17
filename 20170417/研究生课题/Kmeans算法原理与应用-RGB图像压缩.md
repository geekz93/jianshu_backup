## 1 kmeans聚类思想
- **维基百科上的描述**
对于 `X = {x1, x2, ..., xn}` n 个**观测样本**，其中每个样本 x 都是 **d 维向量**，将这 n 个样本划分成 k 个集合 `S = { S1, S2, ..., Sk} (k<=n)`，每个集合使用集合中的样本均值来表示（集合中心 centroid 等于样本均值）。**kmeans算法目的**是：**以**每个 centroid 与集合中所有样本[欧式距离](https://en.wikipedia.org/wiki/Euclidean_space)最小**为标准**，寻找一个最优的集合划分。这个公式概括了之前的描述：(ui 为第 i 个集合的样本均值）
![kmeans_function.png](http://upload-images.jianshu.io/upload_images/3022282-4d1bd8a5a550f793.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


  - **观测样本，d 维向量， 欧式距离**
**例子：**从一张 256x256 像素的[RGB图像](http://baike.baidu.com/item/RGB?fr=aladdin)来解释

![lena256.jpg](http://upload-images.jianshu.io/upload_images/3022282-d223ada0ad0e666d.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)**观测样本x<sub>i</sub>**为图中的每个像素点，共有 256x256=65536 个，RBG图片每个像素点是由（r，g，b）三个通道的值组成（每个值的范围从 0-255），因此每个样本都是**3维向量**。取图中两个像素点 `x1=(179, 121,32)，x2=(137, 50, 75)`，它们的**欧式距离**为：`sum( (x1-x2)^2 ) = (179-137)^2 + (121-50)^2 + (32-75)^2`

## 2 kmean标准算法 - **[Lloyd's algorithm](https://en.wikipedia.org/wiki/Lloyd%27s_algorithm)**
- **算法步骤**
  - **step 1：** **初始化** k 个质心，即设置 k 个 d 维向量，表示要将样本划分成 k 个集合：m<sub>1</sub><sup>(1)</sup>,…,m<sub>k</sub><sup>(1)</sup> 此时，集合中还没有任何样本。m 的上标 (1) 表示中心的更新次数即 step2 中的 t
  > - **几种初始化方法：** 
1.完全随机赋值 
2.随机选择 k 个样本作为初始值 
3.分裂法（先计算所有样本均值得到一个质心，再添加一个微小扰动，使质心 1 分为 2 -> 聚类 -> 再分裂，得到 k 个质心）
  - **step 2：** **聚类**，计算每个观测样本与质心的欧式距离，根据距离最小原则将样本放入 k 个集合中
![](http://upload-images.jianshu.io/upload_images/3022282-900eb93900fb40d6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  - **step 3：** **更新**每个集合的质心，将每个集合的样本均值作为新的质心
![](http://upload-images.jianshu.io/upload_images/3022282-95c293271556c769.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
  - **step 4：**  **判断**是否满足**停止**条件，不满足，则继续进行 step2， step3
> - **停止条件：** 直接设置迭代次数，或者判断质心变化误差很小就视为收敛，退出循环

- 源码分享：[my_kmeans](https://github.com/supertab/gcode/blob/kmeansVQ/kmeans.py)

## 3 k-mean应用：RGB图像压缩
![k-means压缩原理](http://upload-images.jianshu.io/upload_images/3022282-335c7884867ea1b6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240) 这种压缩方法的本质是**[量化矢量(Vector Quaintization)](https://en.wikipedia.org/wiki/Vector_quantization)**，通过 kmeans 聚类得到量化表，将每个像素用量化表中的矢量来表示，然后只要记录每个像素对应的索引值，这样原来使用 24bit 来表示一个像素，现在只需要存储记录索引值所需要的 6bit 就可了，因此实现了压缩图像 
- 压缩测试
k = 2，64，100 即压缩倍数为 12，4，3.42
![](http://upload-images.jianshu.io/upload_images/3022282-c4b0b41f39e515a0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
- 源码分享：[kmeansVQ](https://github.com/supertab/gcode/tree/kmeansVQ)

**参考：**
1.[k-means clusetering wiki](https://en.wikipedia.org/wiki/K-means_clustering)
2.http://blog.pluskid.org/?p=57
