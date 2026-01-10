---
uuid: 20220809092703
created: 2022-08-09T09:27:03
alias: линейный градиент
---

# [[CSS Linear Gradient]]

Градиент в [[HTML and CSS|css]] можно задать с помощью:

`linear-gradient(direction, color1, color2, …)`

where `direction` is the direction of the gradient using keywords or angles. Direction
keywords are written in the form to position where position is either a side of the object or a corner. For example the following linear gradient moves in a straight line to the left edge of the object blending from red to yellow to blue:

`background: linear-gradient(to left, red, yellow, blue);`

To move in a direction other than a side or corner, you can express the direction using an angle value. Angles are measured in degrees with 0deg equal to to top, 90deg equal to to right, 180deg equal to to bottom, and 270deg equal to to left
![[Pasted image 20220809092829.png]]

### Transparency and Gradients
Interesting gradient effects can be achieved using transparent colors so that the background color gradually fades away as it moves in the direction of the gradient. For example, the following style creates a linear gradient that gradually fades away from its initial solid red color:

`linear-gradient(rgba(255, 0, 0, 1), rgba(255, 0, 0, 0))`

Note that since the final color is completely transparent it will adopt the background color of the parent element.

You can also use gradients to create background images that appear to fade by using multiple backgrounds in which the gradient appears on top of an image. For example, the following background style creates a fading background using the `back.png` image file:

`background: linear-gradient(rgb(255, 255, 255, 0), rgb(255, 255, 255, 1)),url(back.png));`

When rendered by the browser, the background image will start as solid but gradually fade to white as the linear gradient proceeds through the element background.

## Gradients and Color Stops

The colors specified in a gradient are evenly distributed so that the following gradient starts with a solid red, solid green appears halfway through the gradient, and finishes with solid blue:

`background: linear-gradient(red, green, blue);`

To change how the colors are distributed, you define color stops, which represent the point at which the specified color stops and the transition to the next color begins. The linear-gradient function using color stops has the general form

`linear-gradient(direction, color-stop1, color-stop2, …)`

Stopping positions can be entered using any of the CSS units of measurement. For example, the following gradient starts with solid red up until 50 pixels from the starting point, red blends to solid green stopping at 60 pixels from the starting point and then blends into solid blue 80 pixels from the start. After 80 pixels, the gradient will remain solid blue to the end of the background.

`linear-gradient(red 50px, green 60px, blue 80px)`

![[Pasted image 20220809093606.png]]

---

## 📇 Additional Metadata

- 🗂 Type:: #type/note
- Source:: [[New Perspectives HTML5 and CSS3 Comprehensive Course]]