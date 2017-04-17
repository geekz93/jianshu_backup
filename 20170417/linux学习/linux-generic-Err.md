在安装unrar，octive的时候报错
出现**原因：** /boot分区空间不足
解决办法：卸载旧的内核
- 查看文件系统还剩多少空间：`df -h` 
- 查看系统中存在的内核：`dpkg --get-selections | grep linux-image` 
- 查看正在使用的内核：`uname -a` 
- 卸载内核：`sudo apt-get purge linux-image-4.4.0-31-generic` 
