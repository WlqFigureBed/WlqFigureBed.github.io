# linux日用命令

查看软件运行：ps -ef | grep

结束进程：kill pid

# 插件配置

## 一、zsh安装

manjaro自带zsh，可以通过`cat /etc/shells`查看安装的shell

设置zsh为默认shell：`chsh -s $(which zsh)`

重启电脑后生效

## 二、oh-my-zsh

为了确保不被拒绝连接，设置hosts文件：

```shell
sudo nano /etc/hosts
## 将下面的内容添加上去：
# GitHub Start
151.101.64.133 raw.githubusercontent.com
# GitHub End
```

接下来安装oh-my-zsh及其插件：

```shell
# 安装oh-my-zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)“

# 安装zsh-syntax-highlighting：提供命令高亮
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

# 安装autosuggestions：记住你之前使用过的命令
git clone git://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions
```

安装主题powerlevel10k

```shell
git clone https://github.com/romkatv/powerlevel10k.git $ZSH_CUSTOM/themes/powerlevel10k
```

启动插件：

```shell
nano ~/.zshrc
## 找到plugins=(git)，修改为：
plugins=(git zsh-syntax-highlighting zsh-autosuggestions sudo extract)
# sudo是ohmyzsh自带的插件，功能是在你输入的命令的开头添加sudo ，方法是双击Esc
# extract也是自带插件，不用再去记不同文件的解压命令，方法是extract +你要解压的文件名

## 找到ZSH_THEME，修改为：
ZSH_THEME="powerlevel10k/powerlevel10k"

# 绑定~为接受建议，在文件末尾添加如下内容：
bindkey '·' autosuggest-accept
```

保存配置：

```shell
source ~/.zshrc
```

重启shell，此时会进入主题设置，按引导进行即可，如果设置后不满意：

```shell
# 重新配置主题
p10k configure
```

## 三、vimplus

安装Vimplus（现代化的vim插件管理工具，开箱即用，不使用vim的可以略过

```shell
git clone https://github.com/chxuan/vimplus.git ~/.vimplus
cd ~/.vimplus
./install.sh
```

查看vim插件：

```shell
vim ~/.vimrc
# 可以看到如下内容，两个call中间的内容就是我们的插件
call plug#begin()
Plug 'preservim/NERDTree'
call plug#end()
```

该vimplus插件默认安装了若干插件，如果安装失败：

```shell
# 进入vim文本编辑器
vim

# 安装所有插件
:PlugInstall

# 更新插件
:PlugUpdate

# 如果你不想更新所有的插件，你可以通过添加插件的名字来更新任何插件:
:PlugUpdate NERDTree
```

## 四、其他

[bat](https://github.com/sharkdp/bat)，该插件用于代替cat，高亮显示：arch安装：`yay -S bat`or`sudo pacman -S bat`

thefuck