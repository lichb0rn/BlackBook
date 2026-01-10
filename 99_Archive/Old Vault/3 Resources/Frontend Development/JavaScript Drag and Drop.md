---
uuid: 20230624062522
created: 2023-06-24T06:25:22
alias: - перетаскивание элементов
---

# [[JavaScript Drag and Drop]]

Обычно, когда мы перетаскиваем элемент, конструкция [[HTML]] не позволяет его отпустить. Чтобы это все же произошло, необходимо предотвратить событие по умолчанию, запрещающее отпускать элемент, который вы собираетесь перетащить - `evet.preventDefault()`:

```html
    <div class="box">1
        <div id="dragme" draggable="true">
            Drag Me Please!
        </div>
    </div>
    <div class="box">2</div>
```

```js
let holderItem;
const boxes = document.querySelectorAll('.box');

boxes.forEach((box) =%3E {
   box.addEventListener('drop', (evt) => {
	    evt.preventDefault();
        if (evt.target.className == 'box') {
           evt.target.appendChild(holderItem);
        }
    });
    box.addEventListener('dragover', (evt) => {
        evt.preventDefault();
    });
});

const draggable = document.getElementById('dragme');
draggable.addEventListener('dragstart', (evt) => {
    holderItem = evt.target;
});
```

---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: [[JavaScript с нуля до профи Библиотека программиста]]
-  🏷️ Tags:: [[JavaScript]], [[Frontend Development]]