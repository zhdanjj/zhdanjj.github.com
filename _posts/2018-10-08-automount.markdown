---
layout: post
title:  "Автомонтирование sshfs"
tags: [linux]
---

# Автомонтирование удаленных каталогов по ssh

`sudo apt-get install sshfs` – позволяет монтировать удаленные фс как каталоги, например:
`sshfs username@server.ru:/home/user mount-point/`
Вместо name@server.ru можно использовать алиас из ~/.ssh/config.

Размонтировать командой `fusermount -u -z mount-point`

# AutomountFUSE
`sudo apt-get install afuse` – автомонтирование каталога.

`afuse -o mount_template="sshfs %r:/ %m" -o unmount_template="fusermount -u -z %m" ~/sshfs/`

Теперь обращения папкам вида username@some.host.ru в каталоге ~/sshfs/ будут вызывать монтирование соответствующей папки.

Источники:
[Удобный доступ к файлам на удаленных хостах](https://habrahabr.ru/post/52310/)

<iframe
  width="100%"
  height="315"
  src="http://www.youtube.com/embed/7ODOwdwY6ko"
  frameborder="0"
  allowfullscreen
>
</iframe>
