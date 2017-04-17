- **im2col伪代码**
计算总块数 N， 训练集中有 M 张样本图
```
N # accout of all blocks
block_size # 8x8
block_set = []
for i in N:
    for each_image in M:
        block_set.append(each_image[i: i+blocksize])
    save(block_set, filename = str(i)
    release block_set # 防止内存溢出
    block_set = []
```

- **tree-kmeans**
经过 im2col 后得到 N 个 block 集合
```
vq_dict_set = []
for i in N:
read file from block_set # 每次只读 1个块集合到内存
set k by prior knowledge # 根据每个块的重要程度设置k值
centorial_set = lbg_algorithm(each_blockSet, k) # 得到 2^k 个中心点
vq_dict_set.append((centorial, k))
```
