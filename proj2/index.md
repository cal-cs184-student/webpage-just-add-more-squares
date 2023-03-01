---
layout: default
title: "Project 2: MeshEdit"
has_children: false
nav_order: 1
mathjax: true
---

![Teapot](../proj2/img/teapot.jpeg)

# Overview

# Part 1
de Casteljau’s algorithm is a recursive algorithm for interpolating points on Bezier curves. For example, if we want to evaluate a Bezier curve at *t*, then at each recursive step, we linearly interpolate between pairs of consecutive control points using *t*. After each step, we end up with one less point. By continuing to recurse until we end up with one point, we find the single interpolated point along the curve!

Here's what the algorithm looks like with 6 original control points.
<!-- table -->

| Control points | Step 1 |
|:---:|:---:|
| ![control-points](../proj2/img/control-points.png) | ![step-1](../proj2/img/de-casteljau-1.png) |

| Step 2 | Step 3|
|:---:|:---:|
| ![step-2](../proj2/img/de-casteljau-2.png) | ![step-3](../proj2/img/de-casteljau-3.png) |

| Step 4 | Result |
|:---:|:---:|
| ![step-4](../proj2/img/de-casteljau-4.png) | ![interpolated](../proj2/img/interpolated-point.png)|

We can also move the control points around and modify the parameter *t*.
![bezier-animation](../proj2/img/bezier-animation.gif){:style="display:block; margin-left: auto; margin-right: auto; width:70%;"}

# Part 2

# Part 3

# Part 4

# Part 5

# Part 6
