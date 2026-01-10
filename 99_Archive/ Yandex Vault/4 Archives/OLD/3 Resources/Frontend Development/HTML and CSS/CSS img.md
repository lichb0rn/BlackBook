Tags: #"" - #"" - [[HTML and CSS]]
\_\_

# img

## Responsive img

Чтобы сделать картинку responsive, нужно установить max-width: 100%, а height: auto. В этом случае изображение будет постраиваться под ширину контейнера, сохряя aspect ration.

```css
img {
	max-width: 100%;
	height: auto;
}
```
