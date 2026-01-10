---
uuid: 20220731203014
created: 2022-07-31T20:30:14
alias:
- смена фона
- change background
---

# [[Change background in css]]

Сниппет для смены бэкграунда
```css
body {
	background-image: url('https://images.unsplash.com/photo-1469474968028-56623f02e42e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1474&q=80');
	background-position: center center;
	background-size: cover;
	transition: 0.4s ease;
}
```

Оверлей
```css
body::before {
	content: '';
	position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 100vh;
	background-color: rgba(0, 0, 0, 0.7);
	z-index: -1;
}
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
- Source:: [[Traversy Media]] Project 18 "Background Slider"
- 🏷️ Tags:: [[OLD/2 Areas/Web Development]], [[Design]]
