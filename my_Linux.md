## Utilities
```shell
# install softwares
sudo apt install git zsh net-tools vim make g++ build-essential cmake ninja-build tmux shadowsocks-libev privoxy gnome-sushi python3-pip curl
# update hosts
sudo sh -c 'echo "140.82.112.3    github.com
199.232.96.133  raw.githubusercontent.com
185.199.108.153 assets-cdn.github.com
199.232.69.194  github.global.ssl.fastly.net
199.232.96.133  raw.github.com
" >> /etc/hosts'
# install and config oh-my-zsh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
vim ~/.zshrc
# change theme to `candy` and set alias `alias l='ls -aF'`

```
## privoxy settings
edit `/etc/privixy/config`, set `forward-socks5  /       127.0.0.1:1080  .
` and `listen-address  0.0.0.0:1081`

## Tmux启动鼠标操作

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


