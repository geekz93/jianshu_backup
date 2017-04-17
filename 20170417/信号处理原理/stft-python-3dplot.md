**说明：**stft函数，绘制3d图
```
from mpl_toolkits.mplot3d import axes3d
import matplotlib.pyplot as plt
from matplotlib import cm
import numpy as np

def stft(signal, wlen, hopstep, zeropad, fc, win):
    slen = len(signal)
    depart_account = (slen-wlen)// hopstep
    fft_account = np.zeros(wlen*zeropad) #fft的点数等于窗长x填零因子
    # 分段fft
    amp = []
    for i in range(depart_account):
        beg = i*hopstep
        end = beg + wlen
        fft_account[0:wlen] = signal[beg:end]*win(wlen)
        temp = np.fft.fft(fft_account)[0:wlen*zeropad//2]
        amp.append(np.abs(temp))
    amp = np.array(amp)
    t = np.linspace( wlen/fc, depart_account/fc, depart_account)
    f = np.linspace(0, fc/2, wlen*zeropad//2)

    return( t, f, amp)
        
        

fc=400
T=20
my_zero=10
t=np.linspace(0,T,fc*T)
x=np.zeros(len(t))
th1=0.25*T*fc
th2=0.5*T*fc
th3=0.75*T*fc
th4=T*fc
x[0:th1]=np.cos(2*np.pi*10*t[0:th1])
x[th1:th2]=np.cos(2*np.pi*25*t[th1:th2])
x[th2:th3]=np.cos(2*np.pi*50*t[th2:th3])
x[th3:th4]=np.cos(2*np.pi*100*t[th3:th4])

at, af, amp = stft(x, 125, 20, 10, fc, np.blackman)

at, af = np.meshgrid(at, af)
amp = amp.transpose()
fig = plt.figure()
ax = fig.add_subplot(121, projection='3d')
ax.plot_wireframe(at, af, amp, rstride=30, cstride=30)
ax1 = fig.add_subplot(122, projection='3d')
ax1.plot_surface(at, af, amp, cmap=cm.coolwarm)
plt.show()
```

![figure_1.png](http://upload-images.jianshu.io/upload_images/3022282-56c4dbd3b08e8ef4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
