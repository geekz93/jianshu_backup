- 2016-12-18
  * 同步gstudy目录
  * 设置bios 启用键盘，在进入系统的时候键盘可以选择了
  * studydate/wavelet-ppt/第一讲/联合时频分析介绍pdf
  名词定义：R Z C，序列和函数的内积空间，Hilbert空间，框架，时频分辨率，带宽
  傅立叶变换的物理意义，短时傅立叶变换原理，步骤
  **Q:** 对于画STFT频谱图的步骤，取点，平移窗函数还不清楚

- 2016-12-19
  * crontab自动任务
  * stft频谱图-未画出
  - fft的理解：为什么两端对称出现
  * fft的泄漏问题http://mp.weixin.qq.com/s?__biz=MzI5NTM0MTQwNA==&mid=2247484164&idx=1&sn=fdaf2164306a9ca4166c2aa8713cacc5&scene=21#wechat_redirect
  * fft窗函数https://zhuanlan.zhihu.com/p/24318554

- 2017-1-2
  * lamb波的传播特性：频散，多模态，群/相速度， 等名词定义了解
  * 研究specgram.py，np.asarray:按步长自动转换数组（尚没弄懂）

- 2017-1-3
  * 同步code和task到github

- 2017-1-4
  * 阅读论文：
2009-板类结构中超声兰姆波检测方法的研究-一般：关于兰母波求解，无收获
1999-无损检测中的超声兰姆波：了解瑞丽-兰母方程的参数，波数、相速度、频厚积、纵波速度/横波速度，的定义
2003-兰姆波频散曲线计算：数值求解瑞丽-兰母方程：自变量为频厚急wd，对于给定wd后求解想速度Cp需要解一个超越方程，使用二分法求解。文中对方程的分段进行了讨论，根据Cp与横波速度Cs的大小比较，通过三角正弦与双曲正弦的转换将方程的虚部去除，得到了分段函数
  * 阅读程序：
绘制平板频散曲线matlab程序：
函数的功能：
**Fedisper:** 主函数，设置有关初值，调佣ss，serfen，aa，aerfen，绘图
**smode:** 瑞丽-兰母方程的分段函数
**ss:** 得到s模式的n组解区间,为之后使用serfen函数求解Cp值做准备, 调用smode
**serfen:** 二分法求解瑞丽-兰母方程，调用smode
**amode,aa,aerfen**和s开头函数功能相同，求解a模式时使用的分段函数不同

- 2017-1-5
  * 准备实验
在钢板上设置不同深度，宽度的缺陷，测试mp能够识别的最小缺陷
  * The Linux Command Line 看到86页

- 2017-1-6
  * 与淘宝店主联系加工钢板 - 发现不能在1-2mm薄板中加工盲孔误差太大
  * 实验测试，在同一块板上打多个槽，回波信号会不会发生干涉，实验结果，从时域图上看由于发生探头是线性探头，即发射的超声波能量集中在一条线上传播，因此，同一块板上只要两个槽之间的距离不是太近，回波的干扰较小
  * 使用abaqus仿真实验，学习中...

- 2017-1-7
  * 整理abaqus使用步骤

- 2017-1-8
  * abaqus仿真实验
将采集到信号作为输入信号进行仿真，实验结果：信号传播速度太快，信号波重叠在一起

- 2017-1-9
  * 阅读文献
2000-超声无损检测若干新进展
2007-金属薄板的超声兰姆波无损检测--看到43页
  * Linux学习
The Linux Command Line 看到90页

- 2017-1-13
  * 卸载贪吃蛇
  * 阅读文献
2005-The_matching_pursuit_approach_based_on_the_modulat

- 2017-1-16
  * 整理gstudy，同步到github中
  * Linux学习
The Linux Command Line 看到103页
  * 线性代数视频 看到第09集

- 2017-1-24
  * 复习线性代数，并做笔记
lesson03-矩阵相乘，矩阵的逆
lesson05-转置、置换、向量空间
lesson06-子空间、列空间和零空间
  * Linux学习
The Linux Command Line 看到112页

- 2017-2-13
  * 线性代数
lesson14-17 矩阵正交、投影、最小二乘法
  * 文献
《Compression of facial images using the K-SVD algorithm》看完摘要，结论
 * Linux
环境配置 p156

- 2017-2-16
  * 线性代数
lesson22,23, 30 矩阵对角化，求矩阵的幂，矩阵的奇异值分解
  * 文献
《Low Bit-Rate Compression of Facial Images》2007 剩下具体算法部分part4未看
  * Linux
12节-Vi 编辑器 p161-175

- 2017-2-17
  * 线性代数
lesson26，28 对称矩阵，正定性，正定矩阵
  * 文献
kmeans聚类算法
  * Linux
12节-Vi编辑器 p176-180
14节-安装包管理 p192-200
15节-存储设备管理 p202-207

- 2017-2-18
  * 树梅派网络配置
  * 将字符传输网站移植到pi中

- 2017-2-19
  * 线性代数
复习lesson14-17 推导投影矩阵，最小二乘法公式
  * 文献
了解“图像超分辨率重建有关知识”
http://www.kancloud.cn/digest/imagesuperresolution
  * Linux
15节-存储设备管理 p208-218

- 2017-2-20
  * 线性代数
lesson29 相似矩阵，诺尔当形
  * 文献
《K-SVD An Algorithm for Designing Overcomplete Dictionaries for Sparse Representation》p1-p12
斯坦福大学机器学习课程 week1-part1 ： 机器学习介绍
  * Linux
16节-网络命令 p222-229
