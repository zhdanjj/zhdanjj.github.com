---
layout: post
title:  "Система координат на странице"
tags: [js]
---

## Размеры элементов
### Метрики
Метрики — свойства элементов, отражающие размеры и отступы элементов в
пикселях.

`element.offsetParent` — содержит ссылку на первый родительский элемент с
нестатичным позиционированием или `BODY`, если таких нет.

`element.offsetLeft/Top` — смещение относительно `element.offsetParent`
*Считаются устаревшими, в разных браузерах может быть разное поведение*

`element.clientLeft/Top` — `padding` **+ скроллбар если есть**, по сути
равно ширине `border`

`element.scrollLeft/Top` — насколько прокручен элемент, т. е. высота скрытой области.
Для `document.documentElement.scrollLeft/Top` могут быть ошибки в некоторых браузерах,
лучше использовать `window.pageX/YOffset`
Можно изменять. Также можно установить с помощью методов:
```javascript
window.scrollTo(pageX,pageY) // абсолютные координаты,
window.scrollBy(x,y) // прокрутить относительно текущего места.
elem.scrollIntoView(options) // прокрутить, чтобы элемент elem стал виден.
// у последнего метода есть параметры, (позволяющие указать плавность
// анимации и позицию вложенного элемента) — 
// https://developer.mozilla.org/ru/docs/Web/API/Element/scrollIntoView
```

`element.offsetWidth/Height` — ширина вместе с `padding`, `border` и 
полосой прокрутки

`element.clientWidth/Height` — ширина + `padding`, без `border` и полосы прокрутки

`element.scrollWidth/Height` — то же, что и `element.clientWidth/Height`, но с
учётом прокрутки, т. е. как если убрать прокрутку и показать всё содержимое целиком

### Element.getBoundingClientRect()
Возвращает [TextRectangle](https://developer.mozilla.org/en-US/docs/Mozilla/Tech/XPCOM/Reference/Interface/nsIDOMClientRect),
состоящий из полей:

`top` - смещение относительно верхнего края **области просмотра** (не документа). Т. е. если страницу
проскроллить, то значение изменится. Чтобы получить значение относительно документа — `top + window.pageYOffset`

`left` - нижнего края

`width` и `height` —  то же, что и `element.offsetWidth/Height`

`bottom === top + height`

`right === left + width`

`x` и `y` — то же, что и `top` и `left`, но работают только в новых браузерах

### Метрики из jQuery
`$(element).width/height()` — как и `element.clientWidth/Height`, но без `padding`

`$(element).innerWidth/height()` — то же, что и `element.clientWidth/Height`

`$(element).outerWidth/height(includeMargin)` — без аргумента как `element.offsetWidth/Height`
Если передать `true`, будет включать `margin`

`$(element).offset()` — возвращает объект с полями `top` и `left`, где  
`left === element.getBoundingClientRect().left + window.pageXOffset`  
`top === element.getBoundingClientRect().top + window.pageYOffset`  

