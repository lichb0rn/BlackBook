---
tags:
  - resource
area: "[[OLD/2 Areas/Web Development]]"
---
# Viewport Units

Вместо `em` и `px` для определения размера текста, можно использовать ==viewport units== для responsive типографии.
Viewport units зависят от размера экрана устройства.

Есть 4 вида юнитов:

- `vw` (viewport width): `10vw` - 10% от viewport width;
- `vh` (viewport height): `3vh` - 3% от viewport height;
- `vmin` (viewport minimum): `70vmin` - 70% от наименьшей величины viewport width или height;
- `vmax` (viewport max): `100vmax` - 100% от наибольшей.

```css
body {
	width: 30vw;
}
```

[[OLD/1 Projects/Design and Develop a killer website with HTML5 and CSS3]]