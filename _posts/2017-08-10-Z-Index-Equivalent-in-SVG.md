---
layout: post
title: "Z-Index Equivalent in SVG"
author: evanbrodie
date: 2017-08-10T12:46:42+00:00
---

To mimic the [z-index CSS property](https://developer.mozilla.org/en/docs/Web/CSS/z-index) in SVG, add the SVG elements to the page in the reverse order that you expect their z-positioning to be set. The subsequent elements added are placed on top of previous elements.

For example, if I were using the React SVG charting library [Victory](https://github.com/FormidableLabs/victory) and I wanted my chart lines to be stacked on top of my chart area shading, I will add them to my component like so:

```jsx
<VictoryChart>
  <VictoryArea ... />
  <VictoryLine ... />
</VictoryChart>
```
