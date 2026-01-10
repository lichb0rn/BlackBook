---
uuid: 20220804093308
created: 2022-08-04T09:33:08
alias: фоновая картинка в css
---

# [[CSS Background-image]]


## `background-repeat`

The default browser behavior is to place the background image at the **top-left corner of the element and repeat the image in both the vertical and horizontal direction** until the background is filled. This process is known as **tiling** because of its similarity to the process of filling up a floor or other surface with tiles

You can specify the type of tiling to be applied to the background image, or even turn off tiling, by applying the following background-repeat style:

`background-repeat: type;`

where `type` is `repeat` (the default), `repeat-x`, `repeat-y`, `no-repeat`, `round`, or
`space`. 
![[Pasted image 20220804093601.png]]


## `background-size`
The size of the background image is equal to the size stored in the image file. To specify a different size, apply the following background-size property:

`background-size: width heigth`

[[064 HTML and CSS|CSS]] also supports the sizing keywords `auto`, `cover`, and `contain`. The `auto` keyword tells the browser to automatically set the width or height value based on the dimensions of the original image. The following style sets the height of the image to 200 pixels and automatically scales the width to keep the original proportions of the image:

`background-size: auto 200px;`

The `cover` keyword tells the browser to resize the image to cover all of the element background while still retaining the image proportions. Depending on the size of the element, this could result in some of the background image being cropped. The `contain` keyword scales the image so that it’s completely contained within the element, even if that means that not all of the element background is covered. 
![[Pasted image 20220804095102.png]]

### `background` property
All of these different background options can be organized in the following background property:
`background: color url(url) position / size repeat attachment origin clip;`
- `color` - background color;
- `url` - source if the image
- `position` - image's position

#### Adding multiple backgrounds
To add multiple backgrounds to the same element, you list the backgrounds in the following comma-separated list:
`background: background1, background2, …;`

```css
header {
	background: url(back2.png) top left no-repeat,
				url(back1.png) bottom right no-repeat,
				rgb(191, 191, 191);
}
```

**Backgrounds are added in the reverse order** in which they’re listed in the style rule. In this style rule, the background color is applied first, the back1.png background image is placed on top of that, and finally the back2.png background image is placed on top of those two backgrounds.

Individual background properties can also contain multiple options placed in a comma-separated list. The following style rule creates the same multiple backgrounds for the header element without using the background property:

```css
header {
	background-image: url(back2.png), url(back1.png);
	background-position: top left, bottom right;
	background-repeat: no-repeat;
	background-color: rgb(191, 191, 191);
}
```

Note that **if a background style is listed once, it is applied across all of the backgrounds.**
Thus the background-color and the background-repeat properties are used in all the backgrounds.

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[New Perspectives HTML5 and CSS3 Comprehensive Course]]