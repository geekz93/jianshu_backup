## 保存二维数组到csv格式和bit格式
```
def list2bit(data, filename):
    import pickle
    with open(filename, 'wb') as f:
        pickle.dump(data,f)

def list2csv(data, filename, flag=0):
    #data 为二维数组
    temp_str = ''
    if flag:
        # 写列
        for each_list in data:
            for element in each_list:
                temp_str = temp_str+str(element)+','
            temp_str += '\n'
    else:    
        # 写行
        for col in range(len(data[len(data)//2])):
            for row in range(len(data)):
                temp_str = temp_str+str(data[row][col])+','
            temp_str += '\n'

    with open(filename, 'w') as f:
        f.write(temp_str)
```
