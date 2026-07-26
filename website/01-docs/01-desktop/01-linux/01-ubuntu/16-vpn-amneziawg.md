---
layout: page
title: Установка amneziawg в Ubuntu Linux
description: Установка amneziawg в Ubuntu Linux
keywords: desktop, linux, ubuntu, editors, vpn, amneziawg
permalink: /desktop/linux/ubuntu/vpn/amneziawg/
---

<br/>

# Установка amneziawg

**Делаю:**  
2026.07.25

<br/>

```shell
$ sudo apt update && sudo apt install resolvconf
```

<br/>

```shell
$ sudo add-apt-repository ppa:amnezia/ppa
$ sudo apt install -y amneziawg amneziawg-tools
```

<br/>

```shell
$ cd ~/tmp
```

<br/>

```shell
$ cat <<EOF > test.conf
[Interface]
PrivateKey = $(awg genkey)
Address = 10.0.0.2/32
Jc = 4
Jmin = 40
Jmax = 70

[Peer]
PublicKey = vP77S5S5S5S5S5S5S5S5S5S5S5S5S5S5S5S5S5S5S5U=
Endpoint = 1.1.1.1:51820
AllowedIPs = 0.0.0.0/0
EOF
```

<br/>

```shell
$ sudo awg-quick up ./test.conf
$ sudo awg-quick down ./test.conf
```

<br/>

### Добавление нормального конфига

https://warp-generator.github.io/

// Пока перестало работать!  
https://github.com/ImMALWARE/bash-warp-generator

<br/>

**Телеграм-боты:**

```
@warp_generator_bot,
@free_vpn_amnezia_bot,
@warpGuardBot.
```

<br/>

```shell
$ sudo awg-quick up ./test.conf
$ sudo awg-quick down ./test.conf
```

<br/>

```shell
$ curl ifconfig.me
2a09:bac5:5157:2373::388:76
```

<br/>

```shell
$ sudo awg show
```
