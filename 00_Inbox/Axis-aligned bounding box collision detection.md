---
tags:
  - type/source
source: "[[Beginning C++ Game Programming]]"
related:
area:
up:
  - "[[Game Development]]"
aliases:
  - AABB
---
Техника определения столкновений AABB широко используется в 2D графике из-за своей простоты и вычислительной эффективности.

```c++
if(objectA.getPosition().right > objectB.getPosition().left
    && objectA.getPosition().left < objectB.getPosition().right ) {   
    // objectA is intersecting objectB on x axis   
// But they could be at different heights   
	if(objectA.getPosition().top < objectB.getPosition().bottom        
        && objectA.getPosition().bottom > objectB.getPosition().top ) {      
            // objectA is intersecting objectB
            // on y axis as well-
			// Collision detected 
        }
}
```

