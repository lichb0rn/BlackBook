---
created: 2021-07-12T15:24:05
aliases:
  - позиционирование css
tags:
  - type/note
topic: "[[064 HTML and CSS|css]]"
source: "[[Tiny CSS Projects]]"
---

# [[css positioning]]


# Positioning an element with CSS

В css элементы имеют свой собственный "каркас", что обычно называется [[CSS Block Model]]. Блочные элементы автоматические начинаются с новой строки (`hn`, `div`, `p`). `inline` элементы остаются "внутри" контента. Такое поведение называется ==normal flow==.

## Свойтсво Position

### Relative позиционирование

`relative` позволяет описать позицию элемента относительно нормального потока страницы с помощью свойств `left`, `right`, `top`, `bottom`.

```css
p {
	position: relative;
	bottom: 10px;
}
```

Параграф будет отодвинут от нижней границы на 10 пикселей.
Изменение позиции через `relative` не меняет нормальный поток.

```css
div {
	position: relative;
	top: 250px;
	left: 450px;
}
```
![[Pasted image 20220730200543.png]]

Размещение других элементов не затронуто изменением позиционирования `div`. Они остаются на своих позициях.

### Absolute позиционирование

`absolute` вырывает элемент из потока и закрепляется его позицию относительно ближайшего ==positioned== предка. Если в родителе не установлено свойство `relative`, браузер будет искать вверх по дереву вплоть до `html`. Если дошло до `html`, то координаты будут отсчитаны от границ окна. 

```css
header {
	position: absolute;
	top: 620px;
	left: 30px;
}
```
![[Pasted image 20220730200909.png]]
![[Pasted image 20220730201310.png]]

Whenever we use `position: absolute`, we take the element out of the regular flow of the page and can set a specific position on the page on which to place the element. The position is calculated based on the closest ancestor with a position value of `relative`. **If none is found, the top left will be the top-left corner of the page.**

What gets a bit confusing here is that **if no values are set to position the element (`top`, `left`, `right`, `bottom`, or `inset`), the element is placed wherever it normally would lie but takes up no space in the flow**. The `height` and `width` of the element are also affected. 

If a value is provided in the CSS, the element maintains that value; otherwise, **it takes up only as much room as it needs**. Even if it’s a block-level element, **it no longer takes up the full width available to it.** Furthermore, if the `width` is set using a relative unit such as percentage, it will be **calculated against the element to which it’s relative**. Figure shows some scenarios for using `position: absolute`:
![[Pasted image 20230926070449.png]]

### Fixed позиционирование

`fixed` выдирает элемент из нормального поток и закрепляет его относительно окна браузера. Элемент будет отставать на своём месте даже при скроллинге.

```css
#navbar {
	position: fixed;
	top: 0;
	left: 0;
	width: 100%;
	background-color: #767676;
}
```