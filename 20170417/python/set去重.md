- set 以hash值作为去重依据，因此list中需要为可hash对象，：字符串，元组等
```
t1 = [11,2]
t2 = [2,45]
t3 = [t1, t2, t1, t1, t2] # 有重复数据
# 先将list转化为tuple
t3 = [tuple(i) for i in t3]
# 去重
r = set(t3)
```
