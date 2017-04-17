## SVD与基本子空间
- A 的四个基本子空间
列空间：Col A
左零空间： Null A<sup>T</sup>
行空间： Row A
零空间： Null A
**四个子空间的关系：** Col A 与Null A<sup>T</sup>正交，Row A 与 Null A正交

- SVD 与四个基本子空间的关系
A 的svd 分解： A = UΣV<sup>-1</sup>
Σ 中有 r 个非零奇异值，与它们对应的 r 个非零左奇异向量 **{ u1, u2, ..., ur }**是 **Col A** 的一组**标准正交基**
**{ u<sub>r+1</sub>, ..., u<sub>m</sub> }** 是 **Null A<sup>T</sup>** 的一组**标准正交基**
右奇异向量 **{v1, v2, ..., vr}** 是 **Row A** 的一组**标准正交基**
**{v<sub>r+1</sub>, ... v<sub>n</sub>} ** 是 **Null A** 的一组**标准正交基**

## SVD与A的伪逆 - Ax=b的最小二乘解
- A 的伪逆定义为：A<sup>+</sup> = V<sub>r</sub>D<sup>-1</sup>U<sub>r</sub><sup>T</sup>
- Ax = b 的解 x'
由于 A<sup>T</sup>A 会使  A 的元素的误差被放大，因此使用 SVD 代替
x' = A<sup>+</sup>b
