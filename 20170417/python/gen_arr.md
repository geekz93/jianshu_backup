```python
import numpy as np
import numpy.random as random

#中间区域
def comp_num(t, x, y, arr, r):
    '''
    t: temp number
    x,y: postion
    arr: arr300x300'''
    # 索引达到上界会溢出
    for i in range(-r, r+1):
        for j in range(-r, r+1):
            if t==arr[x+i][y+j]:
                return False

    return True

# 上,下行 
def row(t,x, y, arr):
    '''
    顶行
    x=0,1,-1
    底行
    x=298,299,0
    '''
    x_index= [0, 1, -1] if x==0 else [298, 299, 0]
    for i in x_index:
        for j in [0, 1, -1]:
            if t==arr[i][y+j]:
                return False
    return True

# 左右
def column(t, x, y, arr):
    y_index=[0, 1, -1] if y==0 else [298, 299, 0]
    for i in [0, 1, -1]:
        for j in y_index:
            if t==arr[x+i][j]:
                return False
    return True

x_max, y_max=300,300 
arr = np.zeros((x_max, y_max))
num=list(range(1,20))
r=1
for x in range(r, x_max-r):
    for y in range(r, y_max-r):
        temp=num.copy()
        while True:
            t=random.choice(temp)
            if comp_num(t, x, y, arr, r):
                arr[x][y]=t
                break
            else:
                temp.remove(t)

# 上下行处理
for x in [0, 299]:
    for y in range(1,y_max-1):
        temp=num.copy()
        while True:
            t=random.choice(temp)
            if row(t, x, y, arr ):
                arr[x][y]=t
                break
            else:
                temp.remove(t)

for y in [0, 299]:
    for x in range(1, x_max-1):
        temp=num.copy()
        while True:
            t=random.choice(temp)
            if column(t, x, y, arr ):
                arr[x][y]=t
                break
            else:
                temp.remove(t)

# print(arr)
```

![image.png](http://upload-images.jianshu.io/upload_images/3022282-b33a94c3b427b982.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
