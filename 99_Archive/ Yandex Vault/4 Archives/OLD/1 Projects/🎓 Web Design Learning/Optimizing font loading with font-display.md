---
uuid: 20230905094241
created: 2023-09-05T09:42:41
aliases:
  - font-display
---

# [[Optimizing font loading with font-display]]

If your main font is a web font, it’s a good idea to request the file upfront by loading it with a link in the head section of your [[HTML and CSS|HTML]] with the `rel` attribute value as preload:
```html
<link
    rel="preload"
    href="fonts/inter.var.woff2"
    as="font"
    type="font/woff2"
    crossorigin
/>
```
Adding a link with `rel="preload"` included in this way triggers a request for the web font early in the critical rendering path, without having to wait for the **CSS Object Model (CSSOM)** to be created.

## font-display
```css
font-display: fallback;
```

The fallback value we have provided sets an extremely short **block period** and a short **swap period**.

Imagine a browser loading our web page in which we have specified a web font for our text. The browser already has the [[HTML and CSS|HTML]] and is parsing the [[HTML and CSS|CSS]], and learns it needs to download a font in order to display the text it has as intended. Before it draws any text to the screen, **it hangs on, waiting for the web font so it can paint the text onto the page as needed**. This **delay is referred to as a FOIT**, standing for **Flash of Invisible Text**.

As soon as the font arrives, the browser parses it and paints the text to the screen accordingly.

Если задержка при загрузке большая, то есть два варианта:
- One option is **to wait for the font to be downloaded**, usually for up to a few seconds but sometimes indefinitely; Safari is the most famous proponent of this option.
- The second option is **to render the text with a system font initially and then replace the font with the correct font** when the browser has it. This redraw of text from system font to the actual intended font is known as a **Flash of Unstyled Text**, or **FOUT** for short.

All the `font-display` setting does is allow us some control over what we would like to see happen. The possible values are:
- `auto` - на усмотрение браузера
- `block` - белый экран до 3-х секунд, а потом правильный шрифт заменит системный
- `swap` - короткий период (около 100мс) на загрузку шрифта, иначе рисуем системный. Когда загрузится, меняем на желаемый
- `fallback` - - This option **prevents a web font from replacing a system font if a set amount of time has passed** (3 seconds is the recommendation). This option blocks for around 100 ms initially and allows a swap for up to 3 seconds, but after that, if the web font subsequently arrives, it doesn’t get applied.
- `optional` - the browser allows a very short duration for the web font to load (100 ms) but no swap period. The result of this is that the browser has the option of canceling the font download if it hasn’t arrived, or if it has, using it for subsequent page loads.

---

## 📇 Additional Metadata
- 🛠️ Status:: #📚
- 🗂 Type:: #type/note
- ℹ️ Source:: [[Responsive Web Design with HTML5 and CSS]]
- 🏷️ Tags:: [[CSS Text Properties]]