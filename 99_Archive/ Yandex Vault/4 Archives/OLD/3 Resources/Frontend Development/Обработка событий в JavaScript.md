---
uuid: 20230722060907
created: 2023-07-22T06:09:07
alias:
- javascript event handling
- handle events
---

# [[Обработка событий в JavaScript]]

Когда происходит событие, браузер создаёт _объект события_, записывает в него детали и передаёт его в качестве аргумента функции-обработчику. Мы можем назначить обработчиком не только функцию, но и объект при помощи `addEventListener`. В этом случае, когда происходит событие, вызывается метод объекта `handleEvent`.

При назначении обработчика в [[HTML and CSS|HTML]], тоже можно использовать объект `event`, вот так:
```html
<button id="elem">Нажми меня </button>

<script>
  elem.addEventListener('click', {
    handleEvent(event) {
      alert(event.type + " на " + event.currentTarget);
    }
  });
</script>
```

Это возможно потому, что когда браузер из атрибута создаёт функцию-обработчик, то она выглядит так: `function(event) { alert(event.type) }`. То есть, её первый аргумент называется `"event"`, а тело взято из атрибута.

## Объект-обработчик: handleEvent

Мы можем назначить обработчиком не только функцию, но и объект при помощи `addEventListener`. В этом случае, когда происходит событие, вызывается метод объекта `handleEvent`.

```html
<button id="elem"> Нажми меня</button>

<script>
  elem.addEventListener('click', {
    handleEvent(event) {
      alert(event.type + " на " + event.currentTarget);
    }
  });
</script>
```

>[!note]
>Как видим, если `addEventListener` получает объект в качестве обработчика, он вызывает `object.handleEvent(event)`, когда происходит событие.

Также можно использовать [[JavaScript Class|класс]]:
```html
<button id="elem">Нажми меня</button>

<script>
  class Menu {
    handleEvent(event) {
      switch(event.type) {
        case 'mousedown':
          elem.innerHTML = "Нажата кнопка мыши";
          break;
        case 'mouseup':
          elem.innerHTML += "...и отжата.";
          break;
      }
    }
  }

  let menu = new Menu();
  elem.addEventListener('mousedown', menu);
  elem.addEventListener('mouseup', menu);
</script>
```

Можно переделать метод `handleEvent`:
```javascript
class Menu {
    handleEvent(event) {
      // mousedown -> onMousedown
      let method = 'on' + event.type[0].toUpperCase() + event.type.slice(1);
      this[method](event);
    }

    onMousedown() {
      elem.innerHTML = "Кнопка мыши нажата";
    }

    onMouseup() {
      elem.innerHTML += "...и отжата.";
    }
  }

  let menu = new Menu();
  elem.addEventListener('mousedown', menu);
  elem.addEventListener('mouseup', menu);
  ```


---

## 📇 Additional Metadata
- 🛠️ Status:: 
- 🗂 Type:: #type/note
- ℹ️ Source:: [[Браузер Документ, события, интерфейсы]]
-  🏷️ Tags:: [[JavaScript]]