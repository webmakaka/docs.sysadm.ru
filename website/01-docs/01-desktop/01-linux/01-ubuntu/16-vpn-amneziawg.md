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

<br/>

**AmneziaWG Config Generator:**  
https://github.com/HereIamGosu/amnezia-config-gen

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

<br/>

### Какой-то AmneziaVPN клиент с GUI

**Делаю:**  
2026.11.07

<br/>

```sheel
$ sudo apt install libxcb-cursor0
```

<br/>

```sheel
// amnezia-client
https://github.com/amnezia-vpn/amnezia-client/releases/

$ wget https://github.com/amnezia-vpn/amnezia-client/releases/download/5.1.0.6/AmneziaVPN_5.1.0.6_linux_x64.run


// Устанавливается в гуи
$ chmod +x ./AmneziaVPN_5.1.0.6_linux_x64.run 
$ ./AmneziaVPN_5.1.0.6_linux_x64.run 


// Если какая-то амнезия залезла в память и не вылазит
// $ sudo killall AmneziaVPN

// запуск
$ AmneziaVPN
```
