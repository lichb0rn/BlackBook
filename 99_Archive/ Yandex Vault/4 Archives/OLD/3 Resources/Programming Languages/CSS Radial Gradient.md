---
uuid: 20220809094026
created: 2022-08-09T09:40:26
alias: радиальный градиент в css
---

# [[CSS Radial Gradient]]

A [[HTML and CSS|css]] radial gradient is a color gradient that starts from a central point and proceeds outward in a series of concentric circles or ellipses. 
![[Pasted image 20220809094119.png]]

Radial gradients are created using the following radial-gradient function.

`radial-gradient(shape size at position, color-stop1, color-stop2, …)`

The `shape` value defines the shape of the gradient and is either `ellipse` (the **default**) or `circle`. The `size` value defines the extent of the gradient as it radiates outward and can be expressed with a [[HTML and CSS|css]] unit of measure, a percentage of the background’s width and height, or with one of the following keywords:
•	`farthest-corner `(the **default**) Gradient extends to the background corner farthest from the gradient’s center.
•	`farthest-side` Gradient extends to background side farthest from the gradient’s center.
•	`closest-corner`	 Gradient extends to the nearest background corner.
•	`closest-side` Gradient extends to the background side closest to the gradient’s center.

The position defines where the gradient radiates from and can be expressed in coordinates using pixels, percentages of the element’s width and height, or with the keywords: `left`, `center`, `right`, `top`, and `bottom`. The default is to place the gradient within the center of the background.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[New Perspectives HTML5 and CSS3 Comprehensive Course]]