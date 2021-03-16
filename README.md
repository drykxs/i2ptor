# How to setup i2p and tor using privoxy

### -1. Always root

#### 0. DISABLE THE X9 (also known as IPV6) 
```
systemctl -w net.ipv6.conf.default.disable_ipv6=1
systemctl -w net.ipv6.conf.all.disable_ipv6=1
systemctl -p
```


### 1. Installs
- apt or yum or dnf or whatever linux/wsl you are using
```
install tor privoxy i2p

```


### 2. setup privoxy (use whatever you want. I dont care, just bkp before edit)
```
cp /etc/privoxy/config /etc/privoxy/config.old
vim /etc/privoxy/config
```

### 2.1 search for 9050 
- For vim:

/9050 

### 2.2 Uncomment the socket.v5 and add the the forward to the i2prouter
```
forward-socks5t   /               127.0.0.1:9050 .
forward          .i2p             localhost:4444 
```
### 2.4 Save 
- For vim:

:x

### 3. Allow i2p to run as root (bkp won't hurt)
- It will be  */etc/init.d/i2p* **OR** */etc/default/i2p* . It depends on your Linux-or-like-flavor
```
cp /etc/init.d/i2p /root/i2p.old
vim /etc/init.d/i2p
```


### 3.1 uncomment the line
ALLOW_ROOT=true

### 3.2 Save as in 2.4

### 4. Start them all
- Here also depends on the flavor, for Debian-like you will run **'service'** command instead
```
systemctl start tor
i2p/i2prouter start
systemctl start privoxy
```

### 5. Setup the proxy
* This depends on your O.S. and XWindow, but what you need is:
```
export http_proxy="http://127.0.0.1:8118"
export https_proxy="https://127.0.0.1:8118"
export ftp_proxy="ftp://127.0.0.1:8118"
export socks_proxy="ftp://127.0.0.1:9050"
```


# BE HAPPY! #

thanks to [@Thiago](https://gitlab.com/Drakul0g)
