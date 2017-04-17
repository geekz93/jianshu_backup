*[PIL handbook](http://effbot.org/imagingbook/image.htm#tag-Image.Image.save)*
*[ALL IN](https://pillow.readthedocs.io/en/latest/handbook/index.html)*


## PIL - Python Image Library
- **压缩，改变尺寸**
```
from PIL import Image`
im=Image.open('photo.jpg')
im.save('cs_phote.jpg',quality=50) #compress - 改变图像质量为50，原图为100
im.resize((200,200)).save('rs_photo.jpg') # resize - 改变尺寸为200x200像素
```
- **裁剪图像** crop

- **PIL将np.array数组与图像对象互换**
```
from PIL import Image
import numpy as np
im = Image.open('photo.jpg')
im_array = np.array(im) # 将Image对象转换为数组
im_Image = Image.fromarray(im_array) # 将数组转换为图像
```

- `im.load()` 得到每个像素的值 使用坐标序列来索引`[0,1]` 索引位于 0 列 1 行的像素值

- **图片格式转换：**转 j2k 的时候 **倍数是序列 [50]**
```
im0 = Image.open("lena.bmp")
im0.save("lena.jpg", quality=50) #保存为 jpeg 格式 quality 范围为 [1, 95]
im0.save("lena.j2k", quality_mode="rates", quality_layers=[10]) #保存为 jpeg2000 格式，压缩比为10
```
