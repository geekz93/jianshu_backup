参考：
[官网文档](http://matplotlib.org/users/pyplot_tutorial.html)
[3d标注](http://codego.net/514108/)
[legend](http://matplotlib.org/users/legend_guide.html)

- 点形线形：
[matplotlib.pyplot.plot](http://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.plot)

- **显示中文：** 
```
from pylab import *
zhfont = mpl.font_manager.FontProperties(fname='/usr/share/fonts/truetype/wqy/wqy-zenhei.ttc')
```

## 单个图像
- `plt.figure(figsize(w, h))` #创建对象，并指定宽度w高度h，默认像素为80ppi，单位为100像素？还是英寸？
- `plt.plot([1,2,3,4], [1,4,9,16], 'ro')`  #指定xy坐标，显示样式
- `plt.axis([0, 6, 0, 20])`  #指定横纵轴 `[xmin, xmax, ymin, ymax]`
- `plt.xlabel('Smarts')`，`plt.ylabel('Probability')` #设置 x 轴和 y 轴的文字
- `plt.title('Histogram of IQ')`

- **设置文字注释：** `plt.text(60, .025, r'$\mu=100,\ \sigma=15$')`
- **不显示坐标轴：** `plt.axis('off')`
- **显示图像：** `plt.show() `
- **保存图像：** `fig.saveimg(imgname)`

## 多幅图中多个图像
* `plt.xx`操作是针对当前`fig`对象，通过`plt.figure(str)`切换到需要操作的图像，通过`plt.subplot(num)`切换到子图像
>   subplot(236)： 图像总数为2行x3列，中的第6幅图
![23x](http://upload-images.jianshu.io/upload_images/3022282-f1e5e39b1d3374b8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


```python
import matplotlib.pyplot as plt
plt.figure(1) # the first figure,也可以为字符串
plt.subplot(211) # the first subplot in the first figure
plt.plot([1, 2, 3])
plt.subplot(212) # the second subplot in the first figure
plt.plot([4, 5, 6])
plt.figure(2) # a second figure
plt.plot([4, 5, 6]) # creates a subplot(111) by default
plt.figure(1) # figure 1 current; subplot(212) still current
plt.subplot(211) # make subplot(211) in figure1 current
plt.title('Easy as 1, 2, 3') # subplot 211 title
```

- 多幅子图：
```
fig=plt.figure()
ax1=fig.add_subplot(311)
```
- 设置横坐标为[0, 100]
`ax1.set_xlim(0,100)`
- 设置x轴标签
`ax1.set_xlabel('x')`
- 设置子图之间的距离
调整子图的横向和纵向间隔
`fig.subplots_adjust(wspace=0.5, hspace=0.3)`
[关于共享横轴和总轴](http://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.subplot)
