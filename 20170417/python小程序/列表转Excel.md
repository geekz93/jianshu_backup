输入二维列表，以csv格式文本保存
```
def list2csv(data, filename):
    #data 为二维数组
    temp_str = ''
    for each_list in data:
        for element in each_list:
            temp_str = temp_str+element+','
        temp_str += '\n'
    try:
        with open(filename, 'x') as f:
            f.write(temp_str)
    except:
        print("File exists...")
```
