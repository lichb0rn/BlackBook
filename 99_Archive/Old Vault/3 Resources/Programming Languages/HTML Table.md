---
uuid: 20220824121614
created: 2022-08-24T12:16:14
alias:
- <table>
- html table
- таблица html
---

# [[HTML Table]]

## Marking a Web Table and Table Rows in [[064 HTML and CSS|html]]

_• To mark a web table and the table rows, enter_

```html
<table>
	<tr>
		table cells
	</tr>
	<tr>
		table cells
	</tr>
</table>
```

## Marking Header Cells and Data Cells
To mark a header cell, enter
```html
<th>content</th>
```

To mark a data cell, enter
```html
<td>content</td>
```

## Collapsing and spacing
The default browser style is to separate the border around the entire table from the borders around individual table cells, creating additional space in the table layout. Another style choice is to collapse the borders into each other.
![[Pasted image 20220824122020.png]]

To choose between the separate or collapsed borders model, apply the following
`border-collapse`  property to the  `table`  element.

`border-collapse: type;`
where `type`: `separate` (default) or `collapse`.

If the separate borders model is used, the spacing between the borders is set by adding the following `border-spacing`  property to the  `table`  element.

`border-spacing: value;`

where  `value`  is the space between the borders in one of the [[064 HTML and CSS|css]] units of measure.
```css
table {
	border-collapse: separate;
	border-spacing: 10px;
}
```

#### Table styles precedence
[[HTML Table Precedence]]

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[New Perspectives HTML5 and CSS3 Comprehensive Course]]