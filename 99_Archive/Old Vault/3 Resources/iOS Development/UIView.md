---
aliases: ["uiview", "UIView"]
---
MOC:  [[UIKit]]

---

# UIView

View - это экземпляр класса UIView, ответственный за прямоугольную область в окне приложения. View обеспечивают отрисовку контента, обслуживание жестов, управление разметкой (layout) и subview.
В иерархии view, родительские view ответсвенны за поизиционирование и определение размеров дочерних view.

## Цикл отрисовки
UIView класс использует модель отрисовки "по требованию". В первое появление view на экране, система  просит view отрисовать контент. Далее система делает снапшот контента и использует его в качестве представления view.

>The [UIView](https://developer.apple.com/documentation/uikit/uiview) class uses an on-demand drawing model for presenting content. When a view first appears on the screen, the system asks it to draw its content. The system captures a snapshot of this content and uses that snapshot as the view’s visual representation. If you never change the view’s content, the view’s drawing code may never be called again. The snapshot image is reused for most operations involving the view. If you do change the content, you notify the system that the view has changed. The view then repeats the process of drawing the view and capturing a snapshot of the new results.

Когда контент view нужно изменить, мы инвалидируем view с помощью функций `setNeedsDisplay()` или `
setNeedsDisplay(_ rect: CGRect)`.

>When the contents of your view change, you do not redraw those changes directly. Instead, you invalidate the view using either the [setNeedsDisplay](https://developer.apple.com/documentation/uikit/uiview/1622437-setneedsdisplay) or [setNeedsDisplayInRect:](https://developer.apple.com/documentation/uikit/uiview/1622587-setneedsdisplayinrect) method. These methods tell the system that the contents of the view changed and need to be redrawn at the next opportunity. The system waits until the end of the current run loop before initiating any drawing operations. This delay gives you a chance to invalidate multiple views, add or remove views from your hierarchy, hide views, resize views, and reposition views all at once. All of the changes you make are then reflected at the same time.

## Геометрия и система координат
Система координа начинается с верхнегов левого угла:
![[Pasted image 20210913202216.png]] 

[[UIWindow|окна]] и view определяют свою систему координат, что позволяет задавать координаты относительно них, а не относительно экрана.
> Because every view and window defines its own local coordinate system, you need to be aware of which coordinate system is in effect at any given time. Every time you draw into a view or change its geometry, you do so relative to some coordinate system. In the case of drawing, you specify coordinates relative to the view’s own coordinate system. In the case of geometry changes, you specify coordinates relative to the superview’s coordinate system.

### Связь между frame, bounds и center
Каждый объект view отслеживает свои размеры и положение с помощью `frame`, `bounds` и `center`:
- `frame` - прямоугольник, который определяет размер и положение view относительно системы координат родителя.
- `bounds` - прямоугольник который определяет размер view в собственной системе координат относительно точки `origin`
- `center` - центр view в координатах superview.

![[Pasted image 20210913203048.png]]
> Although you can change the `frame`, `bounds`, and `center` properties independent of the others, changes to one property affect the others in the following ways: 
> -   When you set the `frame` property, the size value in the `bounds` property changes to match the new size of the frame rectangle. The value in the `center` property similarly changes to match the new center point of the frame rectangle. 
> 
> -   When you set the `center` property, the origin value in the `frame` changes accordingly.
> 
> -   When you set the size of the `bounds` property, the size value in the `frame` property changes to match the new size of the bounds rectangle.