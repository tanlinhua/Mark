# VIM

## Vim 从入门到精通

https://github.com/wsdjeg/vim-galore-zh_cn

## 安装

centos

```shell
yum -y install vim

# 卸载老的vim
yum remove vim-* -y

# 下载第三方yum源
wget -P /etc/yum.repos.d/  https://copr.fedorainfracloud.org/coprs/lbiaggi/vim80-ligatures/repo/epel-7/lbiaggi-vim80-ligatures-epel-7.repo

# install vim
yum  install vim-enhanced sudo -y

# 验证vim版本
rpm -qa |grep vim
```

ubuntu

```shell
sudo apt-get remove vim-common # 如果报错卸载不兼容
sudo apt-get install vim
```

## 安装插件

```
1. 安装插件管理器,下载plug.vim到~/.vim/autoload目录. https://github.com/junegunn/vim-plug,

curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

2. vim ~/.vimrc

" 示例
call plug#begin('~/.vim/plugged')
Plug 'scrooloose/nerdtree'
Plug 'fatih/vim-go'
call plug#end()

3. :source ~/.vimrc
4. :PlugInstall
```

## 插件

https://zhuanlan.zhihu.com/p/139847548

https://github.com/rafi/vim-config

https://github.com/PegasusWang/linux_config

https://github.com/theniceboy/nvim

https://github.com/tao12345666333/vim

## 搜索并优化

> golang vim

> php vim

> vue vim

## 快捷键

https://www.jianshu.com/p/868e63940e11

https://www.cnblogs.com/sinsenliu/p/9353939.html

## .vimrc

```
let mapleader=','
inoremap jj <Esc>

set number
set encoding=utf-8
set foldenable

syntax on

call plug#begin('~/.vim/plugged')

Plug 'w0ng/vim-hybrid'
Plug 'scrooloose/nerdtree'
Plug 'fatih/vim-go'
Plug 'vim-airline/vim-airline'
Plug 'vim-airline/vim-airline-themes'
Plug 'voldikss/vim-floaterm'
Plug 'mhinz/vim-startify'

call plug#end()


let g:go_version_warning = 0

nmap <leader>v :NERDTreeFind<cr>
nmap <leader>g :NERDTreeToggle<cr>
let NERDTreeShowHidden=1
let NERDTreeIgnore = [
            \ '\.git$', '\.hg$', '\.svn$', '\.stversions$', '\.pyc$', '\.pyo$', '\.svn$', '\.swp$',
            \ '\.DS_Store$', '\.sass-cache$', '__pycache__$', '\.egg-info$', '\.ropeproject$',
            \ ]


set background=dark
colorscheme hybrid
```

## PlugInstall 失败

因为中国地区访问像 github 这种国外网站很不稳定, 所以在一般都是采用镜像网站的方式间接访问. 而 vim-plug 下载时都是用的实际网站, 我们可以修改 plug.vim 来将实际网站变为镜像网站, 提高下载成功率.

在 plug.vim 中搜索 github, 修改两条语句，即可成功下载 GitHub 资源。

```
1 将该行
let fmt = get(g:, 'plug_url_format', 'https://git::@github.com/%s.git')
 改为
let fmt = get(g:, 'plug_url_format', 'https://git::@hub.fastgit.org/%s.git')
2 将改行
\ '^https://git::@github\.com', 'https://github.com', '')
改为
\ '^https://git::@hub.fastgit\.org', 'https://hub.fastgit.org', '')
```

上述两个步骤的目是让镜像网站代替实际网站, 这样能有效提高下载成功率。

## vim 常用快捷键

浏览

```
j ：下移一行
k ：上移一行
h ：左移一个字符
l ：右移一个字符
gg ：跳到第一行
G ：跳到最后一行
0 ：左移到行首
$ ：右移到行尾
ctrl + f ：向下翻页
ctrl + b ：向上翻页
ctrl + d ：向下翻半页（ d 代表 down ）
ctrl + u ：向上翻半页（ u 代表 up ）
H ：移动到屏幕最上面（页面本身不动）（ H 代表 high ）
L ：移动到屏幕最下面（页面本身不动）（ L 代表 low ）
M ：移动到屏幕中间行（页面本身不动）（ M 代表 middle ）
zt ：把当前行移动到屏幕最上面（ t 代表 top ）
zb ：把当前行移动到屏幕最下面（ b 代表 bottom ）
z. ：把当前行移动到屏幕中间
:<n> ：跳到第 <n> 行（需要回车）
```

查找

```
/xxx ：向下查找 xxx （需要回车）
?xxx ：向上查找 xxx （需要回车）
n ：查找下一个（方向由 / 或者 ? 决定）
N ：查找上一个（方向由 / 或者 ? 决定）
/\cxxx ：查找 xxx ，不区分大小写
```

编辑

```
i ：在当前字符前（进入编辑模式）
a ：在当前字符后（进入编辑模式）
o ：在当前行下面添加新行（进入编辑模式）
O ：在当前行上面添加新行（进入编辑模式）
x ：删除（剪切）左边一个字符
X ：删除（剪切）右边一个字符
dd ：删除（剪切）当前行
5dd ：从当前行开始，删除（剪切）5行
d$ ：删除（剪切）当前位置到行尾的内容
d0 ：删除（剪切）当前位置到行首的内容
yy ：复制当前行
5yy ：复制当前5行
y$ ：复制当前位置到行尾的内容
y0 ：复制当前位置到行首的内容
p ：对于复制行，在当前行下面粘贴；对于复制内容，在当前位置之后粘贴（ p 代表 paste ）
P ：对于复制行，在当前行上面粘贴；对于复制内容，在当前位置之前粘贴（ P 代表 paste ）
u ：撤销操作，可以连续撤销（ u 代表 undo ）
```

保存和退出

```
:w ：保存
:q ：退出（没有修改）
:q! ：退出（不保存修改）
:wq ：保存并退出
:x ：保存并退出
```

其它

```
:set nu ：显示行号
:set nonu ：不显式行号
```
