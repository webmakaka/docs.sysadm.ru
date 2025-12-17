---
layout: page
title: Настройка виртуальных хостов
description: Настройка виртуальных хостов
keywords: Настройка виртуальных хостов
permalink: /server/linux/webserver/apache/virtual-hosts/
---

# Настройка виртуальных хостов

    $ cp /etc/httpd/conf/httpd.conf /etc/httpd/conf/httpd.conf.backup.$(date +%Y-%m-%d)

<br/>

    $ mkdir /etc/httpd/conf/websites/_IT/
    $ vi /etc/httpd/conf/httpd.conf

<br/>

    ###########################################################
    ######### VIRTUAL HOSTS #################################
    ###########################################################

    ### IT

    include conf/websites/_IT/docs.sysadm.ru.conf

<br/>

    $ vi /opt/httpd/2.4.3/conf/websites/_IT/docs.sysadm.ru.conf

<br/>

    <VirtualHost *:80>
        ServerName docs.sysadm.ru
        ServerAlias www.docs.sysadm.ru
        DocumentRoot /u01/webProjects/_IT/docs.sysadm.ru
        ErrorLog /u01/logs/_IT/docs.sysadm.ru/docs.sysadm.ru-error.log
        CustomLog /u01/logs/_IT/docs.sysadm.ru/docs.sysadm.ru-access.log combined

        <Directory "/u01/webProjects/_IT/docs.sysadm.ru">
            Options All
            AllowOverride All
            Require all granted
        </Directory>

    </VirtualHost>

При ошибке:

    configuration error:  couldn't perform authentication. AuthType not set

Можно закомментировать

    # Require all granted
