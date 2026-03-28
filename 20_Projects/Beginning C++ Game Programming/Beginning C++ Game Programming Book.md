---
tags:
  - type/note
source:
related:
  - "[[Game Development]]"
area:
up:
  - "[[C++ Language]]"
---
## The Game Loop

When we draw all the game objects, we are drawing them to a hidden surface ready to be displayed. The `window.display() `code flips from the previously displayed surface to the newly updated (previously hidden) one. This way, the player will never see the drawing process as the surface has all the sprites added to it. It also guarantees that the scene will be complete before it is flipped. This prevents a graphical glitch known as **tearing**. This process is called [[Double Buffering|double buffering]].
