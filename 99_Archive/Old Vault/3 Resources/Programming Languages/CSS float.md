---
uuid: 20220728082337
created: 2022-07-28T08:23:37
alias:
---

# [[CSS float]]
By default, content is displayed in the page in the order it appears within the [[064 HTML and CSS|css| HTML]] file as part of the normal document flow. Floating an element takes it out of position and places it along the left or right edge of its parent element. Subsequent content that is not floated occupies the space previously taken up by the floated element. 

![[Pasted image 20220728082422.png]]

if sibling elements are floated along the same margin, they are placed alongside each other within a row:

![[Pasted image 20220728082500.png]]

## Clearing a Float
In some layouts, you will want an element to be displayed on a new row, clear of
previously floated objects. To ensure that an element is always displayed below your
floated elements, apply the following `clear` property:

```css
clear: position;
```

where `position` is `left`, `right`, `both`, or `none`.

The default clear value is `none`, which allows the element to be **displayed alongside any floated objects**.

![[Pasted image 20220728083411.png]]

## Container Collapse
A floated element is taken out of the document flow so that it is no longer “part” of the element that contains it. Literally it is floating free of its container. When every element in a container is floated, there is no content left. As far as the browser is concerned, the container is empty and thus **has no height** and **no background to color**, a situation known as **container collapse**. 

![[Pasted image 20220728084734.png]]

One way to fix that problem is to use the after [[CSS pseudo-element]] to add a placeholder element after the footer. The general style rule is

```css
container::after {
	clear: both;
	content: “”;
	display: table;
}
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[New Perspectives HTML5 and CSS3 Comprehensive Course]]