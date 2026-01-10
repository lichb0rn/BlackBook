---
up:
  - "[[Design and Develop a killer website with HTML5 and CSS3]]"
related:
  - "[[Web Development]]"
tags:
  - source/snippet
created: 2024-02-20
---
Эффекта ленты вокруг угла на [[HTML and CSS|css]] можно добиться так:
```css
.pricing-plan {
    border-radius: 11px;
    width: 75%;
}

.pricing-plan--complete {
    background-color: #fdf2e9;
    padding: 4.8rem;
    position: relative;
    overflow: hidden;
}

.pricing-plan--complete::after {
    content: 'Best value';
    position: absolute;
    top: 6%;
    right: -18%;
    text-transform: uppercase;
    font-size: 1.4rem;
    font-weight: 700;
    background-color: #ffd43b;
    padding: 0.8rem 8rem;
    color: #333;
    transform: rotate(45deg);
}
```

![[Pasted image 20240220094027.png|800]]