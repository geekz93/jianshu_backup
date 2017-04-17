编程环境配置: python3.5 + ipython + vim (x86_64 ubuntu16.04.1)
- 安装pip            
`sudo apt-get update`
`sudo apt-get python3-pip`
- 更新pip            
`sudo pip3 install --upgrade pip`
- 安装virtualenv     
`sudo pip3 install virtualenv`
- 创建python3.5虚拟环境
```                  
virtualenv py3env/ && cd py3env/
source bin/activate  
```                  
- 安装python3工具包  
`pip3 install ipython matplotlib numpy scipy pandas`
                     
- 升级vim            
`sudo apt-get install vim -y` 
- 配置vim            
```                  
mkdir -p .vim/bundle/
vi ~/.vimrc          
```                  
- 安装YCM            
下载文件，解压至`~/.vim/bundle/`目录
[download](https://github.com/Valloric/YouCompleteMe#ubuntu-linux-x64)
安装third-package    
`git submodule update --init --recursive`
安装ycm              
```                  
sudo apt-get install build-essential cmake
sudo apt-get install python-dev
cd ~/.vim/bundle/YouCompleteMe
./setup.py           
```
