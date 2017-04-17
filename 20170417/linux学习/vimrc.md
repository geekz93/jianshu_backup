## 无插件版
**不使用code渲染**
```
" no Plug
"--------- 键映射 ------------------------------
let mapleader=";"
nmap <leader>w :w<CR>
nmap <leader>q :q<CR>

"--------- 缩进指示线 indentLine 配置 ----------
let g:indentLine_char='┆'
let g:indentLine_enabled = 1

"set runtimepath+=~/.vim

set nocompatible
"显示行号"
set number
"" 隐藏滚动条"    
set guioptions-=r 
set guioptions-=L
set guioptions-=b
"隐藏顶部标签栏"
"set showtabline=0
""设置字体"
set guifont=Monaco:h13         
syntax on    "开启语法高亮"

let g:solarized_termcolors=256    "solarized主题设置在终端下的设置"
set background=dark        "设置背景色"
"colorscheme solarized 

"set nowrap    "设置不折行(折行：长的一行用多行显示)"
set fileformat=unix    "设置以unix的格式保存文件"
set cindent        "设置C样式的缩进格式"
set tabstop=4    "设置table长度"
set softtabstop=4 "按backspace回退的缩进长度"
set shiftwidth=4        "同上"
set showmatch    "显示匹配的括号"
set scrolloff=5        "距离顶部和底部5行"
set laststatus=2    "命令行为两行"
set fenc=utf-8      "文件编码"
set backspace=2
"set mouse=a        "启用鼠标"
set selection=exclusive
set selectmode=mouse,key
set matchtime=5
set ignorecase        "忽略大小写"
set incsearch
set hlsearch        "高亮搜索项"
set expandtab        "不允许扩展table"
set whichwrap+=,h,l
set autoread
set cursorline        "突出显示当前行"
set cursorcolumn        "突出显示当前列"
```
## 带插件版
- 安装git
- 在家目录中建立`.vim`目录，在该目录中建立`bundle`目录
- 进入`bundle`目录，下载vundle.vim: `git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim`
- 建立vimrc，vim打开任意文件输入：`PluginInstall`

" update 2016-12-15
filetype off
set nocompatible
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()
"YCM需要单独安装后在添加
"Plugin 'Valloric/YouCompleteMe'
Plugin 'VundleVim/Vundle.vim'
Plugin 'Lokaltog/vim-powerline'
Plugin 'scrooloose/nerdtree'
Plugin 'Yggdroot/indentLine'
Plugin 'scrooloose/nerdcommenter'
Plugin 'tomasr/molokai'
call vundle#end()
filetype plugin indent on

"--------- 键映射 ------------------------------
let mapleader=";"
nmap <leader>w :w<CR>
nmap <leader>q :q<CR>
"switch windows

"F2开启和关闭树"
map <F2> :NERDTreeToggle<CR>
map <F4> <leader>ci <CR>

"--------- 树型目录NERDTree配置 ----------------
let NERDTreeChDirMode=1
let NERDTreeShowBookmarks=1 "显示书签
let NERDTreeIgnore=['\~$', '\.pyc$', '\.swp$']  "设置忽略文件类型
let NERDTreeWinSize=25 "窗口大小

"--------- 缩进指示线 indentLine 配置 ----------
let g:indentLine_char='┆'
let g:indentLine_enabled = 1

"--------------基本设置--------------
set previewheight=1 "设置预览窗口(Scratch)显示行数
"set pumheight=15 "设置弹出菜单高度

set number "显示行号"
"" 隐藏滚动条"    
set guioptions-=r 
set guioptions-=L
set guioptions-=b
set showtabline=0 "隐藏顶部标签栏"
set guifont=Monaco:h13 "设置字体"
syntax on    "开启语法高亮"

let g:solarized_termcolors=256    "solarized主题设置在终端下的设置"
set background=dark        "设置背景色"
"colorscheme solarized 

" set nowrap    "设置不折行"
set fileformat=unix    "设置以unix的格式保存文件"
"set cindent        "设置C样式的缩进格式"
set tabstop=4    "设置table长度"
set shiftwidth=4        "同上"
set softtabstop=4 "按backspace回退的缩进长度"
set showmatch    "显示匹配的括号"
set scrolloff=5        "距离顶部和底部5行"
set laststatus=2    "命令行为两行"
set fenc=utf-8      "文件编码"
set backspace=2
"set mouse=a        "启用鼠标"
set selection=exclusive
set selectmode=key
set matchtime=5
set ignorecase        "忽略大小写"
set incsearch
set hlsearch        "高亮搜索项"
set expandtab        "允许扩展table"
set whichwrap+=,h,l
set autoread
set cursorcolumn        "突出显示当前列"
