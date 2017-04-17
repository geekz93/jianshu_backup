```
from scipy.cluster.vq import kmeans, vq
from numpy import array, reshape, zeros
from PIL import Image

vqclst = [2, 10, 100, 256]

im = array(Image.open('stallman.png'))
(height, width, channal) = im.shape
data = reshape(im, (height*width, channal))
# for k in vqclst:
print('generating vq-%d...'%k)
centroids, distor = vq(data, 2)
code, distor = vq(data, centroids)
print('distor: %.3f'% distor.sum())
im_vq = centroids[code, :]
tmp = reshape(im_vq, (height, width, channel))
im_Image = Image.fromarray(tmp)
im_Image.show()


```
