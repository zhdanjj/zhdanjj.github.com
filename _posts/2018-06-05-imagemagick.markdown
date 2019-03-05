---
layout: post
title:  "Работа с изображениями - утилиты из пакета ImageMagick"
tags: [linux]
---

`identify pic.png` – показывает информацию о файле: разрешение, размер и пр.

Удалить 153 пикселя сверху у картинок в `~/pics/screenshots` и положить в `~/pics/cropped`:  
`mogrify -crop 1366x615+0+153 -path ~/pics/cropped ~/pics/screenshots/*`

Уменьшить до разрешения:  
`convert -resize 1920x1920 photo.jpg photo_resized.jpg`

По-умолчанию утилита игнорирует высоту (но ее все равно нужно указать)
и сохраняет соотношения сторон. Если соотношение нужно игнорировать, можно добавить флаг:  
`convert -resize 1920x1920\! photo.jpg photo_resized.jpg`

Если нужно сделать так, чтобы картинка вписывалась
в указанные размеры и сохраняла соотношение:  
`convert -resize 1920x1920\> photo.jpg photo_resized.jpg`

Сжатие jpg:  
`convert -quality 80 photo.jpg photo_compressed.jpg`

Конвертация:  
`covert photo.jpg photo.png`

Вместо `convert` можно использовать `mogrigy`, их отличие в том,
что последний перезаписывает исходный файл.

******

Иногда бывает, что графика приходит только в высоком качестве.
Скрипт для конвертации изображений в текущей и вложенных папках
в обычное разрешение:
```bash
#!/bin/bash

# image@3x.png 🡆 image.png
#                image@2x.png
#                image@3x.png

if [[ ! $( which convert ) ]]; then
  echo 'Error: install ImageMagick'
  exit 1
fi

shopt -s globstar

for image in **/*@3x.*; do
  new_2x_image=$( echo "$image" | sed -e "s/@3x/@2x/" )
  convert -resize 66.66666%  "$image" "$new_2x_image"
done

for image in **/*@2x.*; do
  new_1x_image=$( echo "$image" | sed -e "s/@2x//" )
  convert -resize 50%  "$image" "$new_1x_image"
done
```

***************************************************************

Источники:  
[http://www.imagemagick.org/Usage/resize/](http://www.imagemagick.org/Usage/resize/)  
[http://www.imagemagick.org/script/convert.php](http://www.imagemagick.org/script/convert.php)
