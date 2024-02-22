## Utilities installation
```shell
# change apt's mirror
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
sudo sed -i "s/archive.ubuntu.com/mirrors.aliyun.com/g" /etc/apt/sources.list
# install softwares
sudo apt install git zsh net-tools vim make g++ build-essential cmake ninja-build tmux shadowsocks-libev privoxy gnome-sushi python3-pip curl tree
# update hosts
sudo sh -c 'echo "140.82.112.3    github.com
199.232.96.133  raw.githubusercontent.com
185.199.108.153 assets-cdn.github.com
199.232.69.194  github.global.ssl.fastly.net
199.232.96.133  raw.github.com
" >> /etc/hosts'
# install and config oh-my-zsh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
#vim ~/.zshrc
echo "alias l='ls -aF'" >> ~/.zshrc
echo "alias ll='ls -lahF'" >> ~/.zshrc
# change theme to `candy` and set alias `alias l='ls -aF'`

```
## zsh settings
[zsh 语法高亮以及自动提示](https://blog.csdn.net/qq_42094345/article/details/107958138)

[zsh autosuggestions在tmux环境下高亮问题处理](https://www.mojidong.com/post/2017-05-14-zsh-autosuggestions/)令tmux也可以正确显示各种颜色，尤其是zsh-autosuggestions `echo "export TERM=xterm-256color" >> ~/.zshrc`

[powerlevel10k](https://github.com/romkatv/powerlevel10k#oh-my-zsh)

[git插件造成卡顿](https://www.jianshu.com/p/bc4b8131db05) （据说上述powerlevel10k也可以起到加速作用，待测）

## privoxy settings
edit `/etc/privixy/config`, set `forward-socks5  /       127.0.0.1:1080  .
` and `listen-address  0.0.0.0:1081`

## Tmux settings
### vi风格快捷键
[Vi mode in tmux](https://blog.sanctum.geek.nz/vi-mode-in-tmux/)
```shell
# ~/.tmux.conf
set-window-option -g mode-keys vi
list-keys -T copy-mode-vi
bind-key -T copy-mode-vi 'v' send -X begin-selection
bind-key -T copy-mode-vi 'y' send -X copy-selection-and-cancel
```
### 修改tmux中的shell simulator，以支持多彩显示
[tmux的终端模拟器设置](https://github.com/loctempt/my_Linux/blob/main/%E4%BD%93%E9%AA%8Ccocnvim.md#tmux%E7%9A%84%E7%BB%88%E7%AB%AF%E6%A8%A1%E6%8B%9F%E5%99%A8%E8%AE%BE%E7%BD%AE)

### 启动鼠标操作
```shell
echo "set -g mouse on" > ~/.tmux.conf
# 如果Tmux在运行，则输入`ctrl+b, :`，然后`source ~/.tmux.conf`
```

## Git settings
### Better Git log
```shell
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```
### Git using proxy
[参考这篇文章 - proxy-setting](https://loctempt.github.io/blog_of_xiyuejiang/proxy-setting)

文章内链接已失效，参考下面的ssh代理配置：
```shell
Host 45.77.31.36
   HostName 45.77.31.36
   User root
   # Port 22
   Port 443
   # ProxyCommand nc -v -X 5 -x 192.168.0.116:7890 %h %p
   # ProxyCommand nc -v -x 192.168.0.109:7890 %h %p
   # ProxyCommand nc -v -x 192.168.0.111:1082 %h %p
   # ProxyCommand nc -v -x 192.168.0.108:7890 %h %p
   ProxyCommand nc -v -x 127.0.0.1:7890 %h %p

Host 108.61.246.183
   HostName 108.61.246.183
   User root
   Port 4000
   # Port 22
   ProxyCommand nc -v -x 127.0.0.1:7890 %h %p

Host github.com
   HostName github.com
   User git
   ProxyCommand nc -v -x 127.0.0.1:7890 %h %p
   # ProxyCommand nc -v -x 192.168.0.111:1082 %h %p
```

## vim 添加cocnvim插件
见[体验cocnvim](https://github.com/loctempt/my_Linux/blob/main/%E4%BD%93%E9%AA%8Ccocnvim.md)
