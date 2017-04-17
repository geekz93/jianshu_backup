- [vlines](http://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.vlines)
- 效果：

![figure_1.png](http://upload-images.jianshu.io/upload_images/3022282-a0009cfbf80731a5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- code
```
import matplotlib.pyplot as plt 
import numpy as np          
import numpy.random as rnd                        
x=np.linspace(-np.pi,np.pi,100)
y=np.sin(x**2)              
fig=plt.figure()            
orig=fig.add_subplot(211)
orig.plot(x, y, )           
vax=fig.add_subplot(212) 
vax.plot(x,y, 'b^')         
vax.vlines(x,[0], y, lw=2)                 
plt.show()  
```
- 说明
`vax.vlines(x,[0], y, lw=2) `
x：横坐标
[0]：竖线的起始值
y：纵坐标，竖线的终点
lw：线的宽度
