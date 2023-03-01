---
layout: default
title: "Project 2: MeshEdit"
has_children: false
nav_order: 1
mathjax: true
---

![Teapot](img/teapot.jpeg)

# Overview

# Part 1: 1D Bezier Curves
de Casteljau’s algorithm is a recursive algorithm for interpolating points on Bezier curves. For example, if we want to evaluate a Bezier curve at *t*, then at each recursive step, we linearly interpolate between pairs of consecutive control points using *t*. After each step, we end up with one less point. By continuing to recurse until we end up with one point, we find the single interpolated point along the curve!

Here's what the algorithm looks like with 6 original control points.
<!-- table -->

| Control points | Step 1 |
|:---:|:---:|
| ![control-points](img/control-points.png) | ![step-1](img/de-casteljau-1.png) |

| Step 2 | Step 3|
|:---:|:---:|
| ![step-2](img/de-casteljau-2.png) | ![step-3](img/de-casteljau-3.png) |

| Step 4 | Result |
|:---:|:---:|
| ![step-4](img/de-casteljau-4.png) | ![interpolated](img/interpolated-point.png)|

We can also move the control points around and modify the parameter *t*.
![bezier-animation](img/bezier-animation.gif){:style="display:block; margin-left: auto; margin-right: auto; width:70%;"}

# Part 2: N-Dimensional Separable Bezier Curves

<!-- Briefly explain how de Casteljau algorithm extends to Bezier surfaces and how you implemented it in order to evaluate Bezier surfaces. -->
<!-- Show a screenshot of bez/teapot.bez (not .dae) evaluated by your implementation. -->

# Part 3: Area-Weighted Vertex Normals

<!-- Briefly explain how you implemented the area-weighted vertex normals. -->
<!-- Show screenshots of dae/teapot.dae (not .bez) comparing teapot shading with and without vertex normals. Use Q to toggle default flat shading and Phong shading. -->

# Part 4: Edge Flip

<!-- Briefly explain how you implemented the edge flip operation and describe any interesting implementation / debugging tricks you have used.
Show screenshots of a mesh before and after some edge flips. -->
We used the primer's guidance on edge flip and drew out the before- and after-flip diagrams for a given edge.
The primer's diagram for edge flip is shown below.

<!-- table -->

|:---:|:---:|
| ![edge-flip-before](./img/edge-flip-before.png) | ![edge-flip-after](./img/edge-flip-after.png) |

However, we noticed that there was some strange naming of edges in the primer's diagram. In particular, there was a strange
rotation of h1, h2, h4, and h5. We elected to ignore this rotation for consistency between the before- and after-flip diagrams.
This detail still allowed us to flip edges correctly.

<!-- Write about your eventful debugging journey, if you have experienced one. -->

Our code did not work on first try. We had some holes in our teapot. We tried to use the halfedge pointers and debugging tools
on the GUI and the IntelliJ debugger but this did not end up so useful. In the end, we double-checked our pointer assignments
and found that we had totally forgotten to update the edges and vertices (only doing halfedges)! After we implemented that,
our code worked.

# Part 5: Edge Split

<!-- Briefly explain how you implemented the edge split operation and describe any interesting implementation / debugging tricks you have used. -->



<!-- Show screenshots of a mesh before and after some edge splits. -->
<!-- Show screenshots of a mesh before and after a combination of both edge splits and edge flips. -->
<!-- Write about your eventful debugging journey, if you have experienced one. -->
<!-- If you have implemented support for boundary edges, show screenshots of your implementation properly handling split operations on boundary edges. -->

# Part 6: Loop Subdivision

<!-- Briefly explain how you implemented the loop subdivision and describe any interesting implementation / debugging tricks you have used. -->
<!-- Take some notes, as well as some screenshots, of your observations on how meshes behave after loop subdivision. What happens to sharp corners and edges? Can you reduce this effect by pre-splitting some edges? -->
<!-- Load dae/cube.dae. Perform several iterations of loop subdivision on the cube. Notice that the cube becomes slightly asymmetric after repeated subdivisions. Can you pre-process the cube with edge flips and splits so that the cube subdivides symmetrically? Document these effects and explain why they occur. Also explain how your pre-processing helps alleviate the effects. -->
<!-- If you have implemented any extra credit extensions, explain what you did and document how they work with screenshots. -->