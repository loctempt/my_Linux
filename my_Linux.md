## Utilities
```shell
# install softwares
sudo apt install git zsh net-tools vim make g++ build-essential cmake ninja-build tmux shadowsocks-libev privoxy gnome-sushi python3-pip curl
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



