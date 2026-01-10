---
created: 2022-08-11T20:12:17
aliases:
  - тени в css
  - box-shadow
tags:
  - type/note
topic: "[[New Perspectives HTML5 and CSS3 Comprehensive Course]]"
source: "[[New Perspectives HTML5 and CSS3 Comprehensive Course]]"
---

# [[Box Shadows and Drop Shadows]]

You may wonder why you need a `drop-shadow` [[HTML and CSS|css filter]] if you already have the `box-shadow` property. While they both can be used to add shadowing to a page object, one important difference is that the drop-shadow filter creates a shadow that traces the shape of the object, while the box-shadow property always applies a rectangular shadow. Another important difference is that you can only change the size of a shadow using the box-shadow property. 

Thus, if you want to apply a drop shadow around objects such as text or a circular shape, use the `drop-shadow` filter. However, if you need to create an internal shadow or change the size of the drop shadow shadow, use the `box-shadow` property.

## Box-shadow
```css
box-shadow: offset-x offset-y blur-radius spread-radius color;
```
