## Utilities
```shell
# install softwares
sudo apt install git zsh net-tools vim tmux shadowsocks-libev privoxy gnome-sushi
# install oh-my-zsh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

```
## privoxy settings
edit `/etc/privixy/config`, set `forward-socks5  /       127.0.0.1:1080  .
` and `listen-address  0.0.0.0:1081`
