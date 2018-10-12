---
layout: post
title:  "Set и Array в JS"
tags: [js]
---

**Array** - тип структуры, представляющий блок данных, расположенных
в последовательной памяти, indexed collection.

**Set** - абстрактный тип данных, содержащий только уникальные элементы,
keyed collection.

**Инициализация Array:**

```js
var arr = []; //Empty array
var arr = [1,2,3]; //Array which contains 1,2,3
var arr = new Array(); //empty array
var arr = new Array(1,2,3);//Array which contains 1,2,3
var arr = Array.from("123"); //["1","2","3"]
```
Инициализация конструктором медленнее, чем литералом.

**Инициализация Array:**
> Set([iterable]))

```js
var emptySet = new Set(); 
var exampleSet = new Set([1,2,3]);
```

Set - нет доступа к элементу

**Проверка на вхождение элемента:**

Array - `arr.indexOf(el)`. При отсутствии вернет -1;
в ES6 есть аналог - `arr.includes(el)`.

Set - `s.has(el)`

**Добавление:**
Array - `push(el)` в конец и `unshift(el)` в начало.
Set - `add(el)`

**Удаление:**  

Array:  
`pop()` - удалит последний и вернет его,  
`shift()` - удалит и вернет первый,  
`slice(startIndex, lastIndex)`  

Set:  
`delete(el)`, где `el` сам элемент, не индекс  
`clear()`

