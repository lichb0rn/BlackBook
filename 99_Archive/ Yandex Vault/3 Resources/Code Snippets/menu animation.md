---
uuid: 20220706174911
created: 2022-07-06T17:49:11
alias: анимация меню
---

# [[menu animation]]

Небольшой сниппет, как можно сделать меню на css + javascript:

```css
nav {
	height: 50px;
	background-color: aquamarine;
	width: 100%;
}

nav ul {
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
}

nav ul li {
	list-style-type: none;
	height: 2rem;
	width: 4rem;
	display: flex;
	justify-content: center;
	align-items: center;
	text-align: center;
	background-color: black;
	border: 1px solid red;
	color: white;
	transition: visibility 0.3s linear, opacity 0.3s linear;
	opacity: 1;
}

nav ul li:hover {
	background-color: rgb(0, 0, 0, 0.5);
}

.hidden {
	opacity: 0;
	visibility: hidden;
}
```

```javascript
const menuButton = document.querySelector('#btn');
const menuItems = document.querySelectorAll('.menu-item');
menuButton.addEventListener('click', () => {
	menuItems.forEach((item) => {
		item.classList.toggle('hidden');
	});
}
```


---

## 📇 Additional Metadata

- 🗂 Type:: #type/snippet 
