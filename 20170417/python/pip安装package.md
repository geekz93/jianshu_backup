## 本地安装
- 工具：`pip2pi`
- 生成本地 package：
  * `pip2tgz package/ ipython==5.3.0`
  * `dir2pi packages/`
- 从本地安装：
  * `pip install --index-url=file:///home/zooo/tools_py/packages/simple/ ipython`

## 重新安装package（不使用本地缓存）
`pip install uwsgi -I --no-cache-dir`

## windows 下 pip 安装扩展包
- 升级pip
cmd 中 `python -m pip install -U pip`

- 下载模块：[Package](http://www.lfd.uci.edu/~gohlke/pythonlibs/#pyparsing)

- 安装模块
cmd 中 `python pip install 模块在电脑中的路径`
