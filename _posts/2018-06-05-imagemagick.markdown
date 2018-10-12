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

Источники:  
[http://www.imagemagick.org/Usage/resize/](http://www.imagemagick.org/Usage/resize/)  
[http://www.imagemagick.org/script/convert.php](http://www.imagemagick.org/script/convert.php)
