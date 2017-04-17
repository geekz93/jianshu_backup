> 使用字符串的split方法，如果split中不填参数，则将字符串按照所有的空白字符(space, \t, \n, ...)为分隔字符，得到一个list，并会将空白字符从list中去除

```
import matplotlib.pyplot as plt
def convert_txt(txt):
    with open(txt, 'r') as f:
        data_str = f.read()
        tmp = data_str.split()
        data = [float(x) for x in tmp]
    return data

data = convert_txt('data01.txt')

# plt.plot(data)
# plt.show()
```
