---
layout: page
title: Монтирование жесткого диска в linux
description: Монтирование жесткого диска в linux
keywords: Монтирование жесткого диска в linux
permalink: /desktop/linux/hardware/hdd/mount-disks/
---

# Монтирование жесткого диска в linux

Делаю!  
2026.05.02

<br/>

В Ubuntu 22.04

!!! На диске нет никаких данных.

<br/>

```shell
$ sudo fdisk -l /dev/sd*
```

<br/>

```shell
$ ls /dev/sd*
/dev/sda  /dev/sda1  /dev/sda2  /dev/sdb
```

<br/>

Мне нужно примонтировать диск, подключенный как sdb. На нем нет никаких разделов.

<br/>

```shell
$ sudo fdisk /dev/sdb
```

<br/>

```shell
Command (m for help): [n]
Partition number (1-128, default 1): [p]
Value out of range.
Partition number (1-128, default 1): [1]
First sector (34-1953525134, default 2048): [Enter]
Last sector, +sectors or +size{K,M,G,T,P} (2048-1953525134, default 1953525134): [Enter]

Created a new partition 1 of type 'Linux filesystem' and of size 931,5 GiB.

Command (m for help): [w]
The partition table has been altered.
Calling ioctl() to re-read partition table.
Syncing disks.
```

<br/>

```shell
// Запись на созданный раздел фаловой системы
$ sudo mkfs.ext4 /dev/sdb1
mke2fs 1.46.5 (30-Dec-2021)
Discarding device blocks: done
Creating filesystem with 244190390 4k blocks and 61054976 inodes
Filesystem UUID: 875447e4-0a36-42a5-a3e1-e6ce7ae6e100
Superblock backups stored on blocks:
	32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208,
	4096000, 7962624, 11239424, 20480000, 23887872, 71663616, 78675968,
	102400000, 214990848

Allocating group tables: done
Writing inode tables: done
Creating journal (262144 blocks):
done
Writing superblocks and filesystem accounting information: done
```

<br/>

```shell
$ ls /dev/sd*
/dev/sda  /dev/sda1  /dev/sda2  /dev/sdb  /dev/sdb1
```

<br/>

```shell
$ sudo mkdir /mnt/dsk1
```

 <br/>

```shell
$ sudo blkid /dev/sdb1
/dev/sdb1: UUID="875447e4-0a36-42a5-a3e1-e6ce7ae6e100" BLOCK_SIZE="4096" TYPE="ext4" PARTUUID="9b93e791-01"
```

<br/>

### Запись в fstab (чтобы после каждой загрузки не монтировать заново)

```shell
$ sudo vi /etc/fstab
```

<br/>

```shell
# Goldenfir 1 TB
UUID=875447e4-0a36-42a5-a3e1-e6ce7ae6e100 /mnt/dsk1 ext4 defaults 0 0
```

<br/>

```shell
$ sudo mount /mnt/dsk1/
```

<br/>

Отменяем резервирование 5% для суперпользователя следующей командой. (Если не нужно)

<br/>

```shell
$ sudo tune2fs /dev/sdb1 -m 0
```

<br/>

```shell
$ df -h | grep sdb1
/dev/sdb1       916G   28K  916G   1% /mnt/dsk1
```

<br/>

### Разрешу пользователю писать на диск

```shell
$ sudo chown -R ${USERNAME} /mnt/dsk1
```
