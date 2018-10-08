---
layout: post
title:  "Конфигурация AwesomeWM 4"
---

## Установка
В ubuntu 16.04 по-умолчанию версия 3.5, установка 4 версии из

```bash
sudo add-apt-repository  ppa:klaus-vormweg/awesome -y
sudo apt update
sudo apt install  awesome awesome-extra -y
```

## Настройка
В первую очередь скопировать файл `/etc/xdg/awesome/rc.lua` и папку `/usr/share/awesome/themes` в `~/.config/awesome/`.

## Тема
Изменить тему можно в файле `~/.config/rc.lua`, исправив строку `beautiful.init("/home/me/.config/awesome/themes/zenburn-copy/theme.lua")`. Если нужно поправить тему, лучше скопировать существующую.
В пути нельзя использовать символ домашней директории ~.

## Громкость
Кнопки громкости добавляются в таблицу globalkeys в виде

```lua
awful.key({}, "XF86AudioRaiseVolume", function () awful.spawn("amixer -D pulse sset Master 5%+", false) end),
awful.key({}, "XF86AudioLowerVolume", function () awful.spawn("amixer -D pulse sset Master 5%-", false) end),
awful.key({}, "XF86AudioMute",        function () awful.spawn("amixer -D pulse sset Master toggle", false) end),
```
Виджет громкости с иконкой и управлением мышкой –
https://github.com/streetturtle/awesome-wm-widgets/tree/master/volume-widget
Импортировать его строкой `require('volume.lua')`, затем добавить в разделе
-- Right widgets в настройках wibox’а s.mywibox:setup.

UPD: проще поставить `apt install volumeicon-alsa`

## Раскладка клавиатуры
В Awesome есть встроенный простой виджет, отображающий текущую раскладку. Можно создать строкой

```lua
-- Keyboard map indicator and switcher
mykeyboardlayout = awful.widget.keyboardlayout()
```
и также добавить в wibox.
Указать раскладки и включить переключение языков по Capslock можно командами

```bash
setxkbmap -layout "us,ru"
setxkbmap -option "grp:caps_toggle"
```

## Автозагрузка
Для автозагрузки можно написать bash-скрипт с функцией, позволяющей запускать только один инстанс приложения:

```bash
#!/usr/bin/env bash

function run {
  if ! pgrep $1 ;
  then
    $@&
  fi
}

run some-longrunning-app
source ~/.screenlayout/default.sh
setxkbmap -layout "us,ru"
setxkbmap -option "grp:caps_toggle"
```
Этот скрипт вызывать в `rc.lua` функцией `awful.spawn.with_shell("~/.config/awesome/autorun.sh")`

## 2 монитора и разрешение экрана
Указанить расположение мониторов и их разрешения утилитой `arandr`.
Она создаст `.sh` файл, который нужно добавить в автозагрузку.

Автомонтирование флешек
С помощью udev [отсюда](http://zenux.ru/articles/40/) не завелось, получилось с
[udiskie](https://github.com/coldfix/udiskie). Просто установить и добавить в
автозагрузку. При подключении флешки будет появляться уведомление, а флешка
будет монтироваться по пути `/media/user-name/drive`.

## Менеджер сети
Добавить `nm-applet` в автозагрузку
