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
de Casteljau’s algorithm is a recursive algorithm for interpolating points on Bezier curves. For example, if we want to evaluate a Bezier curve at $t$, then at each recursive step, we linearly interpolate between pairs of consecutive control points using $t$. After each step, we end up with one less point. By continuing to recurse until we end up with one point, we find the single interpolated point along the curve!

Here's what the algorithm looks like with 6 original control points.
<!-- table -->

| Control points | Step 1 |
|:---:|:---:|
| ![control-points](./img/control-points.png) | ![step-1](./img/de-casteljau-1.png) |

| Step 2 | Step 3|
|:---:|:---:|
| ![step-2](./img/de-casteljau-2.png) | ![step-3](./img/de-casteljau-3.png) |

| Step 4 | Result |
|:---:|:---:|
| ![step-4](./img/de-casteljau-4.png) | ![interpolated](./img/interpolated-point.png)|

We can also move the control points around and modify the parameter *t*.
![bezier-animation](./img/bezier-animation.gif){:style="display:block; margin-left: auto; margin-right: auto; width:70%;"}

# Part 2

For Bezier surfaces, each point is represented by a 3D vector and each surface is defined by a grid of these points. Along one direction of the grid, we first group up points along that direction (e.g. one set per row or column) and run 1D de Casteljau's algorithm to interpolate along the Bezier curves defined by each set of control points. We then take the results of these interpolations and use 1D de Casteljau's again to interpolate along the Bezier curve that is defined.

When we implemented this algorithm to interpolate the point with parameters $(u, v)$ along some Bezier surface, we first filled in the `evaluate1D` function that evaluates a point on a Bezier curve using parameter $t$. Then, we used `evaluate1D` and parameter $u$ to evaluate points along each row. Then, we took the resulting points and made a final interpolation with `evaluate1D` and parameter $v$ to get a single point along the Bezier surface.

Here's our teapot generated with Bezier surfaces:

![teapot-bez](./img/teapot-bez.png){:style="display:block; margin-left: auto; margin-right: auto; width:70%;"}


# Part 3

# Part 4

# Part 5

# Part 6
