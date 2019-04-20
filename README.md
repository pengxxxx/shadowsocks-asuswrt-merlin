# Shadowsocks for Asuswrt-Merlin New Gen

shadowsocks-asuswrt-merlin will install `shadowsocks-libev` and `v2ray-plugin` on your Asuswrt-Merlin New Gen(version 382.xx and higher) based router, tested on NETGEAR R7000 and ASUS RT-AC86U.

For server side set up, you can easily install shadowsocks server and v2ray-plugin with docker by [https://github.com/Acris/docker-shadowsocks-libev](https://github.com/Acris/docker-shadowsocks-libev).

## Getting Started

### Prerequisites
- Asuswrt-Merlin New Gen(version 382.xx and higher) based router
- Entware **must** be installed, you can find installation documents on [https://github.com/RMerl/asuswrt-merlin/wiki/Entware](https://github.com/RMerl/asuswrt-merlin/wiki/Entware)
- JFFS partition should be enabled
- ca-certificates should be installed for HTTPS support
- git and git-http should be installed
- wget should be installed

Make sure you have installed all prerequisites software and utils, you can install it by:
```sh
opkg update
opkg upgrade
opkg install ca-certificates git-http wget
```

### Installing
shadowsocks-asuswrt-merlin is installed by running the following commands in your terminal:
```sh
sh -c "$(wget https://raw.githubusercontent.com/Acris/shadowsocks-asuswrt-merlin/master/tools/install.sh -O -)"
```

### Configuration
```sh
# Edit the shadowsocks configuration file
## Ensure `local_address` is your router's IP address.
## We highly recommend enable v2ray-plugin on your server side.
## You can set up your server in several command with:
## https://github.com/Acris/docker-shadowsocks-libev

vi /opt/share/ss-merlin/etc/shadowsocks/config.json

# Edit the shadowsocks-asuswrt-merlin configuration file
## Currently, shadowsocks-asuswrt-merlin support three mode:
## 0: GFW list. 1: Bypass LAN & mainland China. 2: Global mode.
## You can also enable or disable UDP support to change `udp=0` or `udp=1`.
## Ensure your server side support UDP and set `"mode": "tcp_and_udp"`
## in /opt/share/ss-merlin/etc/shadowsocks/config.json if you want to enable UDP support.

vi /opt/share/ss-merlin/etc/ss-merlin.conf

# Start the service
ss-merlin start
```

### Usage
```sh
admin@R7000:/tmp/home/root# ss-merlin 
 Usage: ss-merlin start|stop|restart|upgrade|uninstall
```

### Custom user rules
```
# Block domain
vi /opt/share/ss-merlin/rules/user_domain_name_blocklist.txt

# Force pass proxy
vi /opt/share/ss-merlin/rules/user_domain_name_gfwlist.txt

# Domain whitelist
vi /opt/share/ss-merlin/rules/user_domain_name_whitelist.txt

# IP whitelist
vi /opt/share/ss-merlin/rules/user_ip_whitelist.txt

# Restart service
ss-merlin restart
```

## Credits
Thanks for the following awesome projects ❤️
- [shadowsocks-libev](https://github.com/shadowsocks/shadowsocks-libev)
- [v2ray-plugin](https://github.com/shadowsocks/v2ray-plugin)
- [asuswrt-merlin.ng](https://github.com/RMerl/asuswrt-merlin.ng)
- [Entware](https://github.com/Entware/Entware)
- [asuswrt-merlin-transparent-proxy](https://github.com/zw963/asuswrt-merlin-transparent-proxy)
- [unbound](https://nlnetlabs.nl/projects/unbound/about/)
- [dnsmasq-china-list](https://github.com/felixonmars/dnsmasq-china-list)
- [gfwlist](https://github.com/gfwlist/gfwlist)
- [gfwlist2dnsmasq](https://github.com/cokebar/gfwlist2dnsmasq)
- [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)
- And many more.

## License
```
The MIT License (MIT)

Copyright (c) 2016 Billy Zheng

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.```