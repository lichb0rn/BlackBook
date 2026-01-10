---
uuid: 20220814144633
created: 2022-08-14T14:46:33
alias:
---

# [[Mobile first principle in CSS]]

Пример организации стилей в [[064 HTML and CSS|css]] по принципу mobile first

```css
/* Base Styles */
	style rules
/* Mobile Styles */
@media only screen and (max-width: 480px) {
	style rules
}
/* Tablet Styles */
@media only screen and (min-width: 481px) {
	style rules
}
/* Desktop Styles */
@media only screen and (min-width: 769px) {
	style rules
}
```

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note