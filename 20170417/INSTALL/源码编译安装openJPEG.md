- [github](https://github.com/uclouvain/openjpeg)
- `sudo apt-get install liblcms2-dev  libtiff-dev libpng-dev libz-dev`
- 安装
```
mkdir build
cd build
cmake ../ -DCMAKE_INSTALL_PREFIX=/usr/
make
make install
```
在 cmake 的时候指定 make install 的路径，否则 ubuntu 下默认安装在 `/usr/local/`下，会导致使用 opj_compress 的时候报错，jpegopen2.so not find

- 使用
```
# 压缩 50 倍
opj_compress -i lena.bmp -o lena.j2k -r 50
# 解压
opj_decompress -i lena.j2k -o lena.bmp
``` 
