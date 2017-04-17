python3
```
import time
begtime = time.perf_counter()#精确记时
for i in range(10):
    #print("passtime: %d"%(i+1))
    time.sleep(0.1)#以秒为单位
endtime = time.perf_counter()
print( "time elipse: %s"%(endtime-begtime) )
```
