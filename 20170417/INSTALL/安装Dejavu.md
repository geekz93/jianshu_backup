# Installation of Dejavu

So far Dejavu has only been tested on Unix systems.

* [`pyaudio`](http://people.csail.mit.edu/hubert/pyaudio/) for grabbing audio from microphone
* [`ffmpeg`](https://github.com/FFmpeg/FFmpeg) for converting audio files to .wav format
* [`pydub`](http://pydub.com/), a Python `ffmpeg` wrapper
* [`numpy`](http://www.numpy.org/) for taking the FFT of audio signals
* [`scipy`](http://www.scipy.org/), used in peak finding algorithms
* [`matplotlib`](http://matplotlib.org/), used for spectrograms and plotting
* [`MySQLdb`](http://mysql-python.sourceforge.net/MySQLdb.html) for interfacing with MySQL databases

#### 安装pyaudio
debian/ubuntu：`sudo apt-get install python-pyaudio`
#### 安装ffmpeg
- [github中下载ffmpeg包](https://github.com/FFmpeg/FFmpeg)
- `./configure --disable-yasm`
- `make`
- `make install`

#### 安装pydub
`sudo pip install pydub`

#### 安装python的mysql模块
`sudo apt-get install python-mysqldb`

#### 安装mysql
- `sudo apt-get insatll mysql-sever`
- `sudo apt-get install mysql-client`
