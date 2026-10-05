---
layout: page
title: Инсталляция Brave в Ubuntu
description: Инсталляция Brave в Ubuntu
keywords: linux, ubuntu, Brave, browser, инсталляция
permalink: /desktop/linux/ubuntu/browser/brave/
---

# Инсталляция Brave в Ubuntu

Делаю:  
2026.10.05

<br/>

```shell
$ wget -qO - https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg | sudo tee /etc/apt/keyrings/brave-browser-archive-keyring.gpg


$ echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/brave-browser-archive-keyring.gpg] https://brave-browser-apt-release.s3.brave.com/ stable main" | sudo tee /etc/apt/sources.list.d/brave-browser-release.list

$ sudo apt update && sudo apt install -y brave-browser
```
