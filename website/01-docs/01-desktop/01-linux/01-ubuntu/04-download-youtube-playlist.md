---
layout: page
title: Скачать playlist с youtube в командной строке ubuntu linux (yt-dlp)
description: Скачать playlist с youtube в командной строке ubuntu linux (yt-dlp)
keywords: linux, ubuntu, youtube, скачать, playlist, yt-dlp
permalink: /desktop/linux/ubuntu/download-youtube-playlist/
---

# Скачать playlist с youtube в командной строке ubuntu linux (yt-dlp)

<br/>

Делаю:  
2026.04.19

<br/>

Автозаменой прошелся по командой. М.б. что и не работает.

<br/>

Т.к. youtube забанили в РФ. Можно скачивать в бесплатном <a href="//docs.gitops.ru/tools/clouds/google/google-cloud-shell/run/">google cloud shell</a>, чем я сосбственно сейчас и занимаюсь.

<br/>

**Программа: **
https://github.com/yt-dlp/yt-dlp/wiki/Installation

<br/>

**Установить ffmpeg - иначе могут быть видео и аудио отдельно!** (м.б. и неактуально уже).

<br/>

```shell
$ sudo apt install -y ffmpeg
```

<br/>

```shell
$ curl -fsSL https://deno.land/install.sh | sh
$ source ~/.bashrc
```

<br/>

```shell
$ sudo curl -L https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -o /usr/local/bin/yt-dlp
$ sudo chmod a+rx /usr/local/bin/yt-dlp
```

<!--

<br/>

Можно установить ее с помощью pip3:
    $ sudo pip3 install yt-dlp --upgrade

-->

<br/>

### Поехали скачивать

<br/>

```shell
$ mkdir -p ~/Downloads/myPlaylist && cd ~/Downloads/myPlaylist
```

<br/>

Нужно скачать вот этот плей лист.

https://www.youtube.com/watch?v=DU9K1rIUWrY&list=PLhgRAQ8BwWFaxlkNNtO0NDPmaVO9txRg8

<br/>

Удаляю из url v=<ID> т.е v=DU9K1rIUWrY

<br/>

```shell
// Скачиваю видео лучшего качества из имеющегося:
$ yt-dlp -i -f 'bestvideo[ext=mp4]+bestaudio[ext=m4a]/bestvideo+bestaudio' --merge-output-format mp4 https://www.youtube.com/watch?list=PLhgRAQ8BwWFaxlkNNtO0NDPmaVO9txRg8 --output "%(title)s.%(ext)s"
```

<br/>

output я меняю, т.к. по умолчанию в конце добавляется id видео. Мне это не нужно.
Можно, также использовать такой формат как --output "%(uploader)s%(title)s.%(ext)s"

<br/>

YouTube стал блочить и просить логиниться.

<br/>

**Помогло:**

<br/>

Установка google chrome extension: "Get cookies.txt LOCALLY"

<br/>

Зайти на страницу с video:

<br/>

```
$ vi youtube_cookies.txt
```

<br/>

Скопировать cookie

<br/>

```shell
$ yt-dlp -f "bestvideo+bestaudio/best" \
--merge-output-format mp4 \
--cookies youtube_cookies.txt \
--js-runtimes deno \
"https://www.youtube.com/watch?v=jWtWDAYtyb4"
```

<br/>

**Еще интересные параметры:**

<br/>

    --playlist-start 1 - с какого индекса в плейлисте начать
    -i - игнорить ошибки, вроде скрытого файла.

<br/>

**Можно также выбрать более подходящий формат:**

    yt-dlp -F http://www.youtube.com/watch?v=3JZ_D3ELwOQ
    sample output:

    [youtube] Setting language
    [youtube] 3JZ_D3ELwOQ: Downloading webpage
    [youtube] 3JZ_D3ELwOQ: Downloading video info webpage
    [youtube] 3JZ_D3ELwOQ: Extracting video information
    [info] Available formats for 3JZ_D3ELwOQ:
    format code extension resolution  note
    171         webm      audio only  DASH webm audio , audio@ 48k (worst)
    140         m4a       audio only  DASH audio , audio@128k
    160         mp4       192p        DASH video
    133         mp4       240p        DASH video
    134         mp4       360p        DASH video
    135         mp4       480p        DASH video
    136         mp4       720p        DASH video
    137         mp4       1080p       DASH video
    17          3gp       176x144
    36          3gp       320x240
    5           flv       400x240
    43          webm      640x360
    18          mp4       640x360
    22          mp4       1280x720    (best)

<br/>

You can choose best and type

    $ yt-dlp -f 22 http://www.youtube.com/watch?v=3JZ_D3ELwOQ

<br/>

To get the best video quality (1080p DASH - format "137") and best audio quality (DASH audio - format "140"), you must use the following command:

    $ yt-dlp -f 137+140 http://www.youtube.com/watch?v=3JZ_D3ELwOQ

<br/>

**Подробнее:**
https://unix.stackexchange.com/questions/272868/download-only-format-mp4-on-yt-dlp/272934

<!-- <br/>

### Сообщение о необходимости обновить avconv

    WARNING: Your copy of avconv is outdated and unable to properly mux separate video and audio files, yt-dlp will download single file media. Update avconv to version 10-0 or newer to fix this.

    $ avconv |& grep \ version | awk '{print $3}'
    9.20-6:9.20-0ubuntu0.14.04.1,

    $ sudo add-apt-repository ppa:heyarje/libav-11 && sudo apt-get update
    $ sudo apt-get install -y libav-tools

    $ avconv |& grep \ version | awk '{print $3}'
    11.3-6:11.3-1~trusty, -->

<br/>

### Передать поток в VLC

```
$ yt-dlp -o - https://www.youtube.com/watch?v=5_J7RWLLVeQ | vlc -
```
