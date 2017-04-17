stft：
- 窗函数的长度与fft的精度有关？
- 填零的作用是为了让fft能够显示出超过窗函数长度的频率：
假设：窗函数的长度为10，如果不填0的话，fft计算的数据点只有10点，信号中频率超过10hz的成分无法显示，填0后，将点数补充到
100个点，就能够显示0-100的频率成分了（和频率分辨率这个概念应该不同，只是为了显示作用）

- 时间轴，hopstep：步长与时间坐标轴有关，即整个时间轴按步长分了多少段
- 频率轴： 按照填零的长度分段
- 幅值轴： fft变换的结果，与频率轴对应

### stft impliment
```
n [spectrogram, axisf, axist] = stft(s,win_size,my_step,fc,win,zeropad)
%
%[spectrogram, axisf, axist] = stft(s,win_size,my_step,fc,win,zeropad)
%
% calculate the spectrogram of the signal s
%
%Input s=signal to process;
% win_size= size of the window to calculate the FFT;
% my_step=shift of the window;
% fc=sampling frequency;
% win=type of window (‘boxcar’,‘hamming’, ‘blackman’);
% zeropad=zeropadding factor;
%
%Output: spectrogram = time-frequency matrix
% axisf= vector of frequencies;
% axist= vector of time;
%
% This MATLAB function resides in:
% http://commons.wikimedia.org/wiki/User:Alejo2083/Stft_script
% Produces the following images:
% http://commons.wikimedia.org/wiki/File:STFT_colored_spectrogram_25ms.png
% http://commons.wikimedia.org/wiki/File:STFT_colored_spectrogram_125ms.png
% http://commons.wikimedia.org/wiki/File:STFT_colored_spectrogram_375ms.png
% http://commons.wikimedia.org/wiki/File:STFT_colored_spectrogram_1000ms.png


if nargin<6
    zeropad=1;
end
if nargin<5
    win='boxcar';
end

N=length(s);

%number of iterations
i_tot=floor((N-win_size)/my_step);

%initialization of the output matrix
spectrogram=zeros(floor(win_size*zeropad/2),i_tot);

%create the right window
if isequal(win,'boxcar')
    my_window=ones(win_size,1);
elseif isequal(win,'hamming')
    my_window=hamming(win_size);
elseif isequal(win,'blackman')
    my_window=blackman(win_size);
end

my_window=my_window';

for ii=1:i_tot
    %starting index
    a=1+(ii-1)*my_step;
    %ending index
    b=win_size+(ii-1)*my_step;
    %part of the signal to be processed
    temp=s(a:b);
    %scale with the chosen window
    temp=temp.*my_window;
    %initialize the zero-padded version
    zeropadded=zeros(1,win_size*zeropad);
    %create the zero-padded vector
    zeropadded(1:win_size)=temp;
    %FFT
    zeropadded=abs(fft(zeropadded));
    %get frequencies only once
    zeropadded=zeropadded(1:floor(win_size*zeropad/2));
    %store in the final matrix
    spectrogram(:,ii)=zeropadded';
end

%create axis to be used to plot the output
axisf=linspace(0,fc/2,floor(win_size*zeropad/2));
axist=linspace(win_size/fc,N/fc,ii);
```

### example
```
clear all;

%sampling frequency
fc=400;
%duration of the signal
T=20;
%zero padding factor
my_zero=10;

%generate the signal
t=linspace(0,T,fc*T);
x=zeros(1,length(t));
%thresholds
th1=0.25*T*fc;
th2=0.5*T*fc;
th3=0.75*T*fc;
th4=T*fc;
x(1:th1)=cos(2*pi*10*t(1:th1));
x((th1+1):th2)=cos(2*pi*25*t((th1+1):th2));
x((th2+1):th3)=cos(2*pi*50*t((th2+1):th3));
x((th3+1):th4)=cos(2*pi*100*t((th3+1):th4));

%calculate and show the spectrograms
[spectrogram, axisf, axist]=stft(x,10,1,fc,'blackman',my_zero);
spectrogram=spectrogram/max(spectrogram(:));
figure,imagesc(axist,axisf,spectrogram),
title('Spectrogram with T = 25 ms'),
ylabel('frequency [Hz]'),
xlabel('time [s]'), 
colorbar;

[spectrogram, axisf, axist]=stft(x,50,1,fc,'blackman',my_zero);
spectrogram=spectrogram/max(spectrogram(:));
figure,imagesc(axist,axisf,spectrogram),
title('Spectrogram with T = 125 ms'),
ylabel('frequency [Hz]'),
xlabel('time [s]'), 
colorbar;

[spectrogram, axisf, axist]=stft(x,150,1,fc,'blackman',my_zero);
spectrogram=spectrogram/max(spectrogram(:));
figure,imagesc(axist,axisf,spectrogram),
title('Spectrogram with T = 375 ms'),
ylabel('frequency [Hz]'),
xlabel('time [s]'), 
colorbar;

[spectrogram, axisf, axist]=stft(x,400,1,fc,'blackman',my_zero);
spectrogram=spectrogram/max(spectrogram(:));
figure,imagesc(axist,axisf,spectrogram),
title('Spectrogram with T = 1000 ms'),
ylabel('frequency [Hz]'),
xlabel('time [s]'), 
colorbar;
```
