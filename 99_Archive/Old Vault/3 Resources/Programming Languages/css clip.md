---
uuid: 20220730203137
created: 2022-07-30T20:31:37
alias:
---

# [[css clip]]

Closely related to the `overflow` property is the `clip` property, which defines a rectangular region through which an element’s content can be viewed. Anything that lies outside the boundary of the rectangle is hidden. The syntax of the clip property is 

```css
clip: rect(top, right, bottom, left); 
```

where `top`, `right`, `bottom`, and `left` define the coordinates of  the clipping rectangle. For  example, a `clip` value of `rect(100px, 270px, 260px, 65px)` defines a clip region whose top and bottom boundaries are 100 and 260 pixels from the top edge of the element, and whose right and left boundaries are 270 and 65 pixels from the element’s left edge.
![[Pasted image 20220730203332.png]]

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note