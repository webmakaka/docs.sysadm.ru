---
layout: page
title: Ubuntu - не спрашивать каждый раз пароль при комаде с sudo
description: Ubuntu - не спрашивать каждый раз пароль при комаде с sudo
keywords: desktop, linux, ubuntu, setup, не спрашивать каждый раз пароль при комаде с sudo
permalink: /desktop/linux/ubuntu/setup/do-not-ask-root-password/
---

# Ubuntu - не спрашивать каждый раз пароль при комаде с sudo

<br/>

**Делаю:**  
2026.08.20

<br/>

```
// добавить при необходимости пользователя в группу sudo
$ sudo usermod -aG sudo ${USER}
```

<br/>

```shell
$ sudo vi /etc/sudoers
```

<br/>

```
# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL
```

меняю на:

```shell
# Allow members of group sudo to execute any command
#%sudo   ALL=(ALL:ALL) ALL
%sudo   ALL=(ALL:ALL) NOPASSWD:ALL
```

```shell
:wq!
```

<br/>

```
$ whoami
marley

$ sudo whoami
root
```

<br/>

### В Linux Mint

```
***
#includedir /etc/sudoers.d
<username> ALL=(ALL:ALL) NOPASSWD: ALL
```
