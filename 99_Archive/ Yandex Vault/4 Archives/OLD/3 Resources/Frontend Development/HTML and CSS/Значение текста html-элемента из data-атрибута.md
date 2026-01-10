---
aliases: 
tags:
  - resource
---

MOC: [[JavaScript]]

---

Допустим у нас есть `div` с data-атрибутом. Мы хотим установить значение текста внутри `div` в зависимости от значения атрибута.

html:

```html
<div class="counter-container">
	<i class="fab fa-twitter fa-3x"></i>
	<div class="counter" data-target="12000"></div>
	<span>Twitter Followers</span>
</div>
```

код

```javascript
const updateCounter = () => {
	const target = parseInt(counter.dataset.target);
	const c = parseInt(counter.innerText);

	const increment = target / counterVelocity;
	if (c < target) {
		counter.innerText = `${Math.ceil(c + increment)}`;
		setTimeout(updateCounter, 1);
	} else {
		counter.innerText = target;
	}
};
```

В `counter` у нас содержится `div.counter`.
