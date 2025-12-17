# Исходники сайта [docs.sysadm.ru](https://docs.sysadm.ru)

<br/>

### Вариант для внесения изменений

Инсталлируете docker и docker-compose, далее:

```
$ cd ~
$ mkdir -p ~/projects/docs.sysadm.ru && cd ~/projects/docs.sysadm.ru
$ git clone --depth=1 https://github.com/webmakaka/docs.sysadm.ru.git .
$ docker-compose up
```

<br/>

Остается в браузере подключиться к localhost:80

<br/>

### Запустить docs.sysadm.ru на своем хосте с использованием docker контейнера:

```
$ docker run -i -t -p 80:80 --name docs.sysadm.ru marley/docs.sysadm.ru
```

<br/>

### Как сервис

```
# vi /etc/systemd/system/docs.sysadm.ru.service
```

вставить содержимое файла docs.sysadm.ru.service

```
# systemctl enable docs.sysadm.ru.service
# systemctl start  docs.sysadm.ru.service
# systemctl status docs.sysadm.ru.service
```

http://localhost:4006
