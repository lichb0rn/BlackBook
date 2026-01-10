---
uuid: 20220805102500
created: 2022-08-05T10:25:00
alias: стиль рамки в css
---

# [[CSS border-style]]

[[HTML and CSS|css]] allows you to further define the appearance of borders using the following border styles:
`border-side-style: style;`

![[Pasted image 20220805102551.png]]

Or to specify styles for all four borders use the property: 
`border-style: top right bottom left;`

As with the other border rules, you can modify the style of all borders or combinations of the borders. For example, the following style uses a double line for the top/bottom borders and a single solid line for the left/right borders: `border-style: double solid;`

All of the border styles discussed above can be combined into the following property that formats the width, style, and color of all of the borders `border: width style color;`
where `width` is the thickness of the border, `style` is the style of the border, and `color` is the border color. 

## Border Image
A border image is a border that it is based on a graphic image. The graphic image is sliced into nine sections representing the four corners, the four sides, and the interior piece. The interior piece is discarded because that is where the content of the object will appear; the four corners become the corners of the border and the four sides are either stretched or tiled to fill in the border’s top, right, bottom, and left sides.
![[Pasted image 20220805104942.png|500]]

`border-image: url(url) slice repeat;`
where `url` is the source of the graphic image, `slice` is the width or height of the slices used to create the sides and corners, and `repeat` indicates whether the side slices should be stretched or tiled to cover the border’s four sides. The `repeat` option supports the following values:
•	`stretch`: The slices are stretched to fill each side.
•	`repeat`:	 The slices are tiled to fill each side.
•	`round`:	 The slices are tiled to fill each side; if they don’t fill the sides with an integer number of tiles, the slices are rescaled until they do.
•	`space`:	 The slices are tiled to fill each side; if they don’t fill the sides with an integer
number of tiles, extra space is distributed around the tiles.

The size of the slices is measured either in pixels or as a percentage of the image file width and height. A quirk of this property is that **you should not specify the pixel unit if you want the slices measured in pixels but you must include the % symbol when slices are measured in percentages**.



---

## 📇 Additional Metadata

- 🗂 Type:: #type/note