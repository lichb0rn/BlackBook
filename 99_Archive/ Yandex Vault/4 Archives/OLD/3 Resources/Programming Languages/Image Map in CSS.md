---
uuid: 20220811202037
created: 2022-08-11T20:20:37
alias: карта изображения в css
---

# [[Image Map in CSS]]
Creating an Image Map in [[HTML and CSS|css]]

•	 To create an image map, use 
```css
<map name=”text”>
	hotspots
</map>
```

where `text` is the name of the image map and `hotspots` are the hotspots within the image.

•	 To define each hotspot, use
```css
<area shape=”shape” coords=”coordinates” href=”url” alt=”text” />
```

where `shape` is the shape of the hotspot region, `coordinates` list the points defining the boundaries of the region, `url` is the URL of the hypertext link, and `text` is alternate text that is displayed for non-graphical browsers.

•	 To define a rectangular hotspot, use the shape and attribute values
```css
shape=”rect” coords=”left,top,right,bottom”
```

where `left`, `top` are the coordinates of the top-left corner of the rectangle and `right`, `bottom` are the coordinates of the bottom-right corner.

•	 To define a circular hotspot, use
```css
shape=”circle” coords=”x,y,radius”
```

where `x` and `y` are the coordinates of the center of the circle and `radius` is the circle’s radius.

•	 To define a polygonal hotspot, use
```css
shape=”poly” coords=”x1,y1,x2,y2,…”
```

where `(x1, y1), (x2, y2)`, and so on provide the coordinates of each vertex in the multisided shape.

•	 To define the default hotspot link, use
```css
shape=”default” coords=”0,0,width,height”
```

where `width` and `height` is the width and height of the image.


---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[New Perspectives HTML5 and CSS3 Comprehensive Course]]