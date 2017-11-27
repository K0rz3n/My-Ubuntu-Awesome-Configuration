# Ubuntu config

### 一、普通桌面环境

#### 1.换源
```
	cd  /etc/apt
	cp sources.list sources.list.bak
	vim sources.list
	apt-get update
	apt-get upgrade
```
```
deb http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse
	##测试版源
deb http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse
	# 源码
deb-src http://mirrors.aliyun.com/ubuntu/ xenial main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse
	##测试版源
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-proposed main restricted universe multiverse
	# Canonical 合作伙伴和附加
deb http://archive.canonical.com/ubuntu/ xenial partner
deb http://extras.ubuntu.com/ubuntu/ xenial main
```

#### 安装 oh-my-zsh
##### 安装
	
	sudo apt-get install zsh

##### 设置zsh 为默认的shell
	
	sudo chsh -s $(which zsh)


##### 安装Oh-My-Zsh
	
	sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"

##### 编辑配置文件
	
	vim  /home/k0rz3n/.zshrc
```
ZSH_THEME="random"
ZSH_THEME_RANDOM_CANDIDATES=( "robbyrussell" "agnoster" "ys" )
```

#### 安装zsh 的插件显示历史命令
https://github.com/zsh-users/zsh-autosuggestions

	git clone git://github.com/zsh-users/zsh-autosuggestions ~/.zsh/zsh-autosuggestions

##### 编辑.zshrc文件
在末尾添加以下命令
	
	source ~/.zsh/zsh-autosuggestions/zsh-autosuggestions.zsh


#### 配置vim
##### 备份：
```
	cp  .vimrc  .vimrc.bak
```
##### 编辑 ~/.vimrc 内容如下：
```
set number
set hlsearch
filetype indent on
set fileencodings=ucs-bom,utf-8,gbk,default,latin1
set encoding=utf-8
colorscheme desert


set expandtab
set tabstop=2
set shiftwidth=2
set autoindent
set smartindent


" Map Ctrl-s to save
noremap ```<silent> <C-s>``` :update```<CR>```
vnoremap``` <silent> <C-s> <C-c>```:update```<CR>```
inoremap ```<silent> <C-s> <C-o>```:update```<CR>```

```
##### 安装Vundle，这样才能方便安装插件：

	mkdir ~/.vim/bundle
	git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim

然后修改~/.vimrc，在最前面添加Vundle的代码
	
	set nocompatible              " 去除VI一致性,必须要添加
	filetype off                  " 必须要添加

	" 设置包括vundle和初始化相关的runtime path
	set rtp+=~/.vim/bundle/Vundle.vim
	call vundle#begin()
	" 另一种选择, 指定一个vundle安装插件的路径
	"call vundle#begin('~/some/path/here')

	" 让vundle管理插件版本,必须
	"Plugin 'VundleVim/Vundle.vim'
	
	" 以下范例用来支持不同格式的插件安装.
	" 请将安装插件的命令放在vundle#begin和vundle#end之间.
	" Github上的插件
	" 格式为 Plugin '用户名/插件仓库名'
	"Plugin 'tpope/vim-fugitive'
	" 来自 http://vim-scripts.org/vim/scripts.html 的插件
	" Plugin '插件名称' 实际上是 Plugin 'vim-scripts/插件仓库名' 只是此处的用户名可以省略
	"Plugin 'L9'
	" 由Git支持但不再github上的插件仓库 Plugin 'git clone 后面的地址'
	"Plugin 'git://git.wincent.com/command-t.git'
	" 本地的Git仓库(例如自己的插件) Plugin 'file:///+本地插件仓库绝对路径'
	"Plugin 'file:///home/gmarik/path/to/plugin'
	" 插件在仓库的子目录中.
	" 正确指定路径用以设置runtimepath. 以下范例插件在	sparkup/vim目录下
	"Plugin 'rstacruz/sparkup', {'rtp': 'vim/'}
	" 安装L9，如果已经安装过这个插件，可利用以下格式避免命名冲突
	"Plugin 'ascenator/L9', {'name': 'newL9'}

	" 你的所有插件需要在下面这行之前
	call vundle#end()            " 必须
	filetype plugin indent on    " 必须 加载vim自带和插件相应的语法和文件类型相关脚本
	" 忽视插件改变缩进,可以使用以下替代:
	"filetype plugin on
	"
	" 常用的命令
	" :PluginList       - 列出所有已配置的插件
	" :PluginInstall     - 安装插件,追加 `!` 用以更新或使用 :PluginUpdate
	" :PluginSearch foo - 搜索 foo ; 追加 `!` 清除本地缓存
	" :PluginClean      - 清除未使用插件,需要确认; 追加 `!` 自动批准移除未使用插件
	"
	" 查阅 :h vundle 获取更多细节和wiki以及FAQ
	" 将你自己对非插件片段放在这行之后

将想要安装的插件，按照地址填写方法，将地址填写在vundle#begin和vundle#end之间就可以

##### 安装以下插件：

nerdtree：文件和目录浏览。
tagbar：函数列表。
echofunc：了解函数参数。
vim-airline：强大的状态栏和Tagbar。
ctrlp: 代码和文件模糊查找。
syntastic：支持各种语言的语法检查。
fugitive：git集成。
tabular: 文本对齐。
vim-youcompleteme 自动补齐杀器
matchit

	$ sudo apt-get install vim-youcompleteme
	$ vim-addons install youcompleteme
	$ sudo apt-get install vim-ctrlp vim-fugitive vim-syntastic vim-tabular
	$ vim-addons install ctrlp
	$ vim-addons install matchit

##### 然后修改~/.vimrc，在最前面添加Vundle的代码，然后在相应部分填写要安装的插件：
 
	Github上的插件
	 格式为 Plugin '用户名/插件仓库名'

	 Plugin 'scrooloose/nerdtree'
	 Plugin 'majutsushi/tagbar'
	 Plugin 'mbbill/echofunc'
	 Plugin 'vim-airline/vim-airline'
	 Plugin 'universal-ctags/ctags.git'
	 Plugin 'kien/ctrlp.vim'
	 Plugin 'scrooloose/nerdcommenter.git'
	 Plugin 'vim-syntastic/syntastic.git'
	 Plugin 'tpope/vim-fugitive.git'
	 Plugin 'godlygeek/tabular.git'
	 Plugin 'vim-scripts/matchit.zip.git'

然后：PluginInstall

##### 然后是插件配置。

为tagbar提供ctags:
```
$ sudo apt-get install exuberant-ctags
让syntastic支持Javascript:
$ sudo apt-get install npm
$ sudo ln -s /usr/bin/nodejs /usr/bin/node
$ sudo npm install -g jshint
让syntastic支持css:
$ sudo npm install -g csslint 
```

##### 然后编辑~/.vimrc添加插件的配置：
```
" NERDTree
map ```<C-n>``` :NERDTreeToggle```<CR>```
" Tagbar
nmap ```<F8>``` :TagbarToggle```<CR>```
" Airline
let g:airline#extensions#tabline#enabled = 1
let g:airline#extensions#tabline#buffer_idx_mode = 1
nmap ```<leader>1 <Plug>```AirlineSelectTab1
nmap ```<leader>2 <Plug>```AirlineSelectTab2
nmap ```<leader>3 <Plug>```AirlineSelectTab3
nmap``` <leader>4 <Plug>```AirlineSelectTab4
nmap ```<leader>5 <Plug>```AirlineSelectTab5
nmap ```<leader>6 <Plug>```AirlineSelectTab6
nmap ```<leader>7 <Plug>```AirlineSelectTab7
nmap ```<leader>8 <Plug>```AirlineSelectTab8
nmap ```<leader>9 <Plug>```AirlineSelectTab9
nmap ```<leader>- <Plug>```AirlineSelectPrevTab
nmap ```<leader>+ <Plug>```AirlineSelectNextTab
```
如果想让airline更漂亮也可以安装powerline字体，但个人认为没必要:
	
	$ sudo apt-get install fonts-powerline

配置 Gvim 也是类似 只是配置文件换了而已
	
	sudo apt install vim-gnome

#### 最终的.vimrc
##### .vimrc
```
set nocompatible              " 去除VI一致性,必须要添加:
filetype off                  " 必须要添加

" 设置包括vundle和初始化相关的runtime path
set rtp+=~/.vim/bundle/Vundle.vim
call vundle#begin()

" 另一种选择, 指定一个vundle安装插件的路径
"call vundle#begin('~/some/path/here')


" 让vundle管理插件版本,必须
Plugin 'VundleVim/Vundle.vim'

" 以下范例用来支持不同格式的插件安装.
" 请将安装插件的命令放在vundle#begin和vundle#end之间.

" Github上的插件
" 格式为 Plugin '用户名/插件仓库名'
"Plugin 'tpope/vim-fugitive'
Plugin 'scrooloose/nerdtree'
Plugin 'majutsushi/tagbar'
Plugin 'mbbill/echofunc'
Plugin 'vim-airline/vim-airline' 
Plugin 'universal-ctags/ctags.git'
Plugin 'kien/ctrlp.vim'
Plugin 'scrooloose/nerdcommenter.git'
Plugin 'vim-syntastic/syntastic.git'
Plugin 'tpope/vim-fugitive.git'
Plugin 'godlygeek/tabular.git'
Plugin 'vim-scripts/matchit.zip.git'


" 来自 http://vim-scripts.org/vim/scripts.html 的插件
" Plugin '插件名称' 实际上是 Plugin 'vim-scripts/插件仓库名' 只是此处的用户名可以省略
"Plugin 'L9'


" 由Git支持但不再github上的插件仓库 Plugin 'git clone 后面的地址'
"Plugin 'git://git.wincent.com/command-t.git'



" 本地的Git仓库(例如自己的插件) Plugin 'file:///+本地插件仓库绝对路径'
"Plugin 'file:///home/gmarik/path/to/plugin'

" 插件在仓库的子目录中.
" 正确指定路径用以设置runtimepath. 以下范例插件在sparkup/vim目录下
"Plugin 'rstacruz/sparkup', {'rtp': 'vim/'}


" 安装L9，如果已经安装过这个插件，可利用以下格式避免命名冲突
"Plugin 'ascenator/L9', {'name': 'newL9'}



" 你的所有插件需要在下面这行之前
call vundle#end()            " 必须
filetype plugin indent on    " 必须 加载vim自带和插件相应的语法和文件类型相关脚本


" 忽视插件改变缩进,可以使用以下替代:
"filetype plugin on
"


" 常用的命令
" :PluginList       - 列出所有已配置的插件
" :PluginInstall     - 安装插件,追加 `!` 用以更新或使用 :PluginUpdate
" :PluginSearch foo - 搜索 foo ; 追加 `!` 清除本地缓存
" :PluginClean      - 清除未使用插件,需要确认; 追加 `!` 自动批准移除未使用插件
"
"" 查阅 :h vundle 获取更多细节和wiki以及FAQ
" 将你自己对非插件片段放在这行之后



set number
set hlsearch
filetype indent on
set fileencodings=ucs-bom,utf-8,gbk,default,latin1
set encoding=utf-8
colorscheme desert
syntax on


set expandtab
set tabstop=2
set shiftwidth=2
set autoindent
set smartindent


" Map Ctrl-s to save
noremap <silent> <C-s> :update<CR>
vnoremap <silent> <C-s> <C-c>:update<CR>
inoremap <silent> <C-s> <C-o>:update<CR>

" NERDTree
map <C-n> :NERDTreeToggle<CR>
" Tagbar
nmap <F8> :TagbarToggle<CR>
" Airline
let g:airline#extensions#tabline#enabled = 1
let g:airline#extensions#tabline#buffer_idx_mode = 1
nmap <leader>1 <Plug>AirlineSelectTab1
nmap <leader>2 <Plug>AirlineSelectTab2
nmap <leader>3 <Plug>AirlineSelectTab3
nmap <leader>4 <Plug>AirlineSelectTab4
nmap <leader>5 <Plug>AirlineSelectTab5
nmap <leader>6 <Plug>AirlineSelectTab6
nmap <leader>7 <Plug>AirlineSelectTab7
nmap <leader>8 <Plug>AirlineSelectTab8
nmap <leader>9 <Plug>AirlineSelectTab9
nmap <leader>- <Plug>AirlineSelectPrevTab
nmap <leader>+ <Plug>AirlineSelectNextTab

```
#### Ubuntu下一款极好的扁平化主题Flatabulous

为了安装这款主题，你必须首先安装Ubuntu tweak tool(译者注:一款管理软件,不过你也可以使用Unity Tweek Tool)。它可以通过命令行方便的安装：
终端
	
	sudo add-apt-repository ppa:tualatrix/ppa
	sudo apt-get update
	sudo apt-get install unity-tweak-tool

主目录里新建一个叫做.theme的文件夹
	
	mkdir .themes

Dash面板

对于图标，我使用ultra-flat-icons这个主题。它包括蓝色（推荐），橙色和薄荷绿三种颜色。你可以通过以下命令来安装它：

    sudo add-apt-repository ppa:noobslab/icons
    sudo apt-get update
    sudo apt-get install ultra-flat-icons
根据你的颜色偏好。我推荐了这款扁平化图标，不过你也可以看看Numix和Flattr。

现在进入你的Dash面板，找到Ubuntu Tweek然后启动它。找到主题选项，选择Flatabulous主题。找到图标选项，选择ultra-flat。接下来重启你的电脑，应该就可以了。

#### 启动器的隐藏
打开"系统设置"，点击"外观"选项
点击"行为"标签
#### 自定义快捷键
系统设置中键盘
打开终端 Ctrl+shift

#### 系统监视器conky
```
sudo apt-get install conky
sudo apt-get install conky-all(必不可少)
在/home/你的文件夹/创建一个文件.conkyrc
```
##### .conkyrc
``` 
#set to yes if you want Conky to be forked in the background
 background no

 cpu_avg_samples 2
 net_avg_samples 2

 out_to_console no

# X font when Xft is disabled, you can pick one with program xfontsel
#font 7x12
#font 6x10
#font 7x13
#font 8x13
#font 7x12
#font *mintsmild.se*
#font -*-*-*-*-*-*-34-*-*-*-*-*-*-*
#font -artwiz-snap-normal-r-normal-*-*-100-*-*-p-*-iso8859-1

# Use Xft?
 use_xft yes

# Xft font when Xft is enabled
 xftfont Sans:size=10

 own_window_transparent no
#own_window_colour hotpink
# Text alpha when using Xft
 xftalpha 0.8

# on_bottom yes

# mail spool
#mail_spool $MAIL

# Update interval in seconds
update_interval 1
# Create own window instead of using desktop (required in nautilus)
own_window yes
own_window_transparent yes
own_window_hints undecorated,below,sticky,skip_taskbar,skip_pager
own_window_type override

# Use double buffering (reduces flicker, may not work for everyone)
double_buffer yes

# Minimum size of text area
minimum_size 260 5
maximum_width 400

# Draw shades?
draw_shades no

# Draw outlines?
draw_outline no

# Draw borders around text
draw_borders no

# Stippled borders?
stippled_borders no

# border margins
#border_margin 4

# border width
border_width 1

# Default colors and also border colors
default_color white
default_shade_color white
default_outline_color white

# Text alignment, other possible values are commented
#alignment top_left
#minimum_size 10 10
gap_x 15
gap_y 70
alignment top_right
#alignment bottom_left
#alignment bottom_right

# Gap between borders of screen and text

# Add spaces to keep things from moving about?  This only affects certain objects.
use_spacer none

# Subtract file system buffers from used memory?
no_buffers yes

# set to yes if you want all text to be in uppercase
uppercase no

# none, xmms, bmp, audacious, infopipe (default is none)
# xmms_player bmp

# boinc (seti) dir
# seti_dir /opt/seti

# Possible variables to be used:
#
#      Variable         Arguments                  Description                
#  acpiacadapter                     ACPI ac adapter state.                   
#  acpifan                           ACPI fan state                           
#  acpitemp                          ACPI temperature.                        
#  adt746xcpu                        CPU temperature from therm_adt746x       
#  adt746xfan                        Fan speed from therm_adt746x             
#  battery           (num)           Remaining capasity in ACPI or APM        
#                                    battery. ACPI battery number can be      
#                                    given as argument (default is BAT0).     
#  buffers                           Amount of memory buffered                
#  cached                            Amount of memory cached                  
#  color             (color)         Change drawing color to color            
#  cpu                               CPU usage in percents                    
#  cpubar            (height)        Bar that shows CPU usage, height is      
#                                    bar's height in pixels                   
#  downspeed         net             Download speed in kilobytes              
#  downspeedf        net             Download speed in kilobytes with one     
#                                    decimal                                  
#  exec              shell command   Executes a shell command and displays    
#                                    the output in torsmo. warning: this      
#                                    takes a lot more resources than other    
#                                    variables. I'd recommend coding wanted   
#                                    behaviour in C and posting a patch :-).  
#  execi             interval, shell Same as exec but with specific interval. 
#                    command         Interval can't be less than              
#                                    update_interval in configuration.        
#  fs_bar            (height), (fs)  Bar that shows how much space is used on 
#                                    a file system. height is the height in   
#                                    pixels. fs is any file on that file      
#                                    system.                                  
#  fs_free           (fs)            Free space on a file system available    
#                                    for users.                               
#  fs_free_perc      (fs)            Free percentage of space on a file       
#                                    system available for users.              
#  fs_size           (fs)            File system size                         
#  fs_used           (fs)            File system used space                   
#  hr                (height)        Horizontal line, height is the height in 
#                                    pixels                                   
#  i2c               (dev), type, n  I2C sensor from sysfs (Linux 2.6). dev   
#                                    may be omitted if you have only one I2C  
#                                    device. type is either in (or vol)       
#                                    meaning voltage, fan meaning fan or temp 
#                                    meaning temperature. n is number of the  
#                                    sensor. See /sys/bus/i2c/devices/ on     
#                                    your local computer.                     
#  kernel                            Kernel version                           
#  loadavg           (1), (2), (3)   System load average, 1 is for past 1     
#                                    minute, 2 for past 5 minutes and 3 for   
#                                    past 15 minutes.                         
#  machine                           Machine, i686 for example                
#  mails                             Mail count in mail spool. You can use    
#                                    program like fetchmail to get mails from 
#                                    some server using your favourite         
#                                    protocol. See also new_mails.            
#  mem                               Amount of memory in use                  
#  membar            (height)        Bar that shows amount of memory in use   
#  memmax                            Total amount of memory                   
#  memperc                           Percentage of memory in use              
#  new_mails                         Unread mail count in mail spool.         
#  nodename                          Hostname                                 
#  outlinecolor      (color)         Change outline color                     
#  pre_exec          shell command   Executes a shell command one time before 
#                                    torsmo displays anything and puts output 
#                                    as text.                                 
#  processes                         Total processes (sleeping and running)   
#  running_processes                 Running processes (not sleeping),        
#                                    requires Linux 2.6                       
#  shadecolor        (color)         Change shading color                     
#  stippled_hr       (space),        Stippled (dashed) horizontal line        
#                    (height)        
#  swapbar           (height)        Bar that shows amount of swap in use     
#  swap                              Amount of swap in use                    
#  swapmax                           Total amount of swap                     
#  swapperc                          Percentage of swap in use                
#  sysname                           System name, Linux for example           
#  time              (format)        Local time, see man strftime to get more 
#                                    information about format                 
#  totaldown         net             Total download, overflows at 4 GB on     
#                                    Linux with 32-bit arch and there doesn't 
#                                    seem to be a way to know how many times  
#                                    it has already done that before torsmo   
#                                    has started.                             
#  totalup           net             Total upload, this one too, may overflow 
#  updates                           Number of updates (for debugging)        
#  upspeed           net             Upload speed in kilobytes                
#  upspeedf          net             Upload speed in kilobytes with one       
#                                    decimal                                  
#  uptime                            Uptime                                   
#  uptime_short                      Uptime in a shorter format               
#
#  seti_prog                         Seti@home current progress
#  seti_progbar      (height)        Seti@home current progress bar
#  seti_credit                       Seti@hoome total user credit


# variable is given either in format $variable or in ${variable}. Latter
# allows characters right after the variable and must be used in network
# stuff because of an argument
#${font Dungeon:style=Bold:pixelsize=10}I can change the font as well
#${font Verdana:size=10}as many times as I choose
#${font Perry:size=10}Including UTF-8,
# stuff after 'TEXT' will be formatted on screen
#${font Grunge:size=12}${time %a  %b  %d}${alignr -25}${time %k:%M}


TEXT
${color white}SYSTEM ${hr 1}${color}

Hostname: $alignr$nodename
Kernel: $alignr$kernel
Uptime: $alignr$uptime
Temp: ${alignr}${acpitemp}°C

CPU: ${alignr}${freq dyn} MHz
Processes: ${alignr}$processes ($running_processes running)
Load: ${alignr}$loadavg

CPU1 ${alignr}${cpu cpu1}%
${cpubar 4 cpu1}
CPU2 ${alignr}${cpu cpu2}%
${cpubar 4 cpu2}

Ram ${alignr}$mem / $memmax ($memperc%)
${membar 4}
swap ${alignr}$swap / $swapmax ($swapperc%)
${swapbar 4}

Highest CPU $alignr CPU%  MEM%
${top name 1}$alignr${top cpu 1}   ${top mem 1}
${top name 2}$alignr${top cpu 2}   ${top mem 2}
${top name 3}$alignr${top cpu 3}   ${top mem 3}

Highest MEM $alignr CPU%  MEM%
${top_mem name 1}$alignr${top_mem cpu 1}   ${top_mem mem 1}
${top_mem name 2}$alignr${top_mem cpu 2}   ${top_mem mem 2}
${top_mem name 3}$alignr${top_mem cpu 3}   ${top_mem mem 3}

${color white}FILE SYSTEM ${hr 1}${color}

Root: ${alignr}${fs_free /} / ${fs_size /}
${fs_bar 4 /}
Home: ${alignr}${fs_free /home} / ${fs_size /home}
${fs_bar 4 /home}

${color white}NETWORK ${hr 1}${color}

Down ${downspeed wlan0} k/s ${alignr}Up ${upspeed wlan0} k/s
${downspeedgraph wlan0 25,107} ${alignr}${upspeedgraph wlan0 25,107}
Total ${totaldown wlan0} ${alignr}Total ${totalup wlan0}

#${color white}WEATHER ${hr 1}${color}

#${execi 3600 python ~/.conkydir/conkyForecast.py --location=CHXX0101 --datatype=CN}
#${font Weather:size=44}${color gold}${execi 3600 python ~/.conkydir/conkyForecast.py --location=CHXX0101 --datatype=WF}${font}${color}${voffset -20}${offset 18}${execi 3600 python ~/.conkydir/conkyForecast.py --location=CHXX0101 --datatype=CC}${offset 10}${execi 3600 python ~/.conkydir/conkyForecast.py --location=CHXX0101 --datatype=HT}${offset 10}${execi 3600 python ~/.conkydir/conkyForecast.py --location=CHXX0101 --datatype=WS} ${font Arrows:size=10}${execi 3600 python ~/.conkydir/conkyForecast.py --location=CHXX0101 --datatype=BF}$font
#${offset 60}Sol: ${color}${execi 3600 python ~/.conkydir/conkyForecast.py --location=CHXX0101 --datatype=SR}-${execi 3600 python ~/.conkydir/conkyForecast.py --location=CHXX0101 --datatype=SS}
#${font Weather:size=26}${execi 3600 python ~/.conkydir/conkyForecast.py --location=CHXX0101 --datatype=WF --startday=1 --endday=4 --spaces=1}${font}
#${execi 3600 python ~/.conkydir/conkyForecast.py --location=CHXX0101 --datatype=HT --startday=1 --endday=4 --spaces=11} 
```


### i3wm 桌面环境
详细讲解在 YouTobe
视频一https://www.youtube.com/watch?v=j1I63wGcvU4
视频二https://www.youtube.com/watch?v=8-S0cWnLBKg
视频三https://www.youtube.com/watch?v=ARKIwOlazKI
详细笔记
http://blog.csdn.net/RichardYan314/article/details/52648670

#### 安装 i3  
	
	sudo apt-get install -y i3
第一次进入会让你选择 Mod键（windows 建议选择alt，如果后期想换可以删除配置文件，这样下次重新进入就会重新让你选择,也可以手动 执行命令   i3-config-wizard）


#### 设置锁屏快捷键 Mod+X
	cd ~/.config/i3
	vim config
在文件末尾添加
	bindsym  $mod + x  exec  i3lock
刷新i3(使一些配置生效)
	Mod+Shift+R
#### 更换背景
```
cd ~ 
mkdir Picture
```
把图片放在里面

	sudo apt-get install -y  feh
进入配置文件   
	exec_always   feh --bg-scale 图片绝对路径

###### 注意：vim 没有行号的时候可以输入命令 :set number

#### 安装图形化页面布局
	sudo apt-get install  -y arandr

#### 配置小图标
下载
https://github.com/FortAwesome/Font-Awesome/releases
```
cd Downloads
unzip  font-Awesome-4.7.0.zip
cd   font-Awesome-4.7.0.zip
cd fonts
mkdir  ~/.fonts
mv  fontawesome-webfont.ttf ~/.fonts
```
复制下面链接里面的图片到需要的地方，注销
http://fontawesome.io/cheatsheet/


#### 下载字体
https://github.com/supermarin/YosemiteSanFranciscoFont
```
unzip  YosemiteSanFranciscoFont-master.zip
cd  YosemiteSanFranciscoFont-master
mv *.ttf   ~/.fonts
vim ~/.config/i3/config
```
把字体部分替换成
```
font pango: System San Francisco Display 11
（实际上我觉得原始的字体很好看）
```

#### 下载  lxappearance 
```
sudo apt-get install -y lxappearance
图形化界面调整样式
```
改变颜色
挑选颜色的网站
http://www.colorpicker.com
还有一些别人写好的dotfiles
	 
	 bindsym $mod+r mode "resize"
 
	 set $bg-color                           #4b0082
	 set $inactive-bg-color                  #2f343f
	 set $text-color                         #f3f4f5
	 set $inactive-text-color                #676E7D
	 set $urgent-bg-color                    #E53935
 
	 #window color
	 #                         border               background              text                          indicator
 
	client.focused            $bg-color            $bg-color               #e0ffff                       #00ff00
	client.unfocused          $iancative-bg-color  $inactive-bg-color      $inactive-text-color          #00ff00
	client.focused_inactive   $iancative-bg-color  $inactive-bg-color      $inactive-text-color          #00ff00
	client.urgent             $urgent-bg-color     $urgent-bg-color        $text-color                   #00ff00
	
	hide_edge_borders both


#### 设置其他的颜色

	bar {
         #status_command i3status
         status_command i3blocks -c /etc/i3blocks.conf
 
         tray_output primary
         colors{
                 background #2f343f
                 separator #757575
                 #                      border                  background          text
                 focused_workspace      $bg-color               $bg-color           $text-color
                 inactive_workspace     $inactive-bg-color      inactive-bg-color   $inactive-text-color
                 urgent_workspace       $urgent-bg-color        $urgent-bg-color    $text-color
 
           }

#### 改变firefox 的主题
arc-firefox-theme
https://github.com/horst3180/arc-firefox-theme
下载release 
然后安装


#### 安装thunar 
	sudo  apt-get install -y thunar
安装 图标
	sudo apt-get install -y gnome-icon-theme-full
图形化文件管理系统


#### 安装arc 主题
https://github.com/horst3180/arc-theme

	sudo sh -c "echo 'deb http://download.opensuse.org/repositories/home:/Horst3180/xUbuntu_16.04/ /' > /etc/apt/sources.list.d/arc-theme.list"
	sudo apt-get update
	sudo apt-get install arc-theme
	wget -nv https://download.opensuse.org/repositories/home:Horst3180/xUbuntu_16.04/Release.key -O Release.key
	sudo apt-key add - < Release.key
	sudo apt-get update


#### 下载moka.icons
https://snwh.org/moka/download
	
	sudo add-apt-repository ppa:moka/daily
	sudo apt-get update
	sudo apt-get install moka-icon-theme faba-icon-theme faba-mono-icons

#### 更改 Mod+D 的样式
##### 第一种

	bindsym_always exec	dmenu_run -nb black -sb tomato -l 10
##### 第二种

#### 下载 rofi
	
	apt-get install -y rofi 
	rofi   -show  run

配置文件修改

	# start dmenu (a program launcher)
	bindsym $mod+d exec rofi -show run -lines 5 -eh 2 -width 100 -padding 420 -opacity "85" -bw 0 -bc "$bg-color" -bg "$inactive-bg-color" -fg "$text-colo    r" -hlbg "#6495ed" -hlfg "#eeee00" font "System San Francisco Display 18"


#### 安装 compton
	sudo apt-get install -y compton
配置文件添加
	
	exec_always compton -f


#### i3lock  screen
	sudo apt-get install pkg-config libxcb1 libpam-dev libcairo-dev libxcb-composite0 libxcb-composite0-dev libxcb-xinerama0-dev libev-dev libx11-dev libx11-xcb-dev libxkbcommon0 libxkbcommon-x11-0 libxcb-dpms0-dev libxcb-image0-dev libxcb-util0-dev libxcb-xkb-dev libxkbcommon-x11-dev libxkbcommon-dev
参考github
https://github.com/ShikherVerma/i3lock-multimonitor
https://github.com/Lixxia/i3lock

	bindsym $mod+x exec i3lock -i ~/.config/i3/atimg.jpg  -c '#2f343f' -o '#191d    0f' -l '#ffffff' -e 


#### 修改bar 的样式
见其他颜色这一部分的配置文件

	status_command i3blocks -c /etc/i3blocks.conf

time 部分的 
	interval =1

volume 部分

	interval=1
	command=/usr/share/13block/volume 5 pulse




