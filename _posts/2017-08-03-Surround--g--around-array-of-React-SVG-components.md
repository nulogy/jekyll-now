---
layout: post
title: "Surround <g> around array of React SVG components"
author: evanbrodie
date: 2017-08-03T02:58:31+00:00
---

It is a typical practice when writing a React component that renders a list/array of components to surround these components around a `<div>` tag. This is because React does not directly support rendering arrays of components.

This practice will not work if the React components will deep-render SVG elements instead of HTML markup. The solution instead will be to wrap the array of SVG-based child components around `<g>` tags (which stands for *group* in SVG).

https://www.smashingmagazine.com/2015/12/generating-svg-with-react/
