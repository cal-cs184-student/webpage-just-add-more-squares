---
layout: post
title: "Project 1: Rasterizer"
---

For this project, we explored many fundamental ideas in computer graphics, including rasterization, transformations, barycentric coordinates, change-of-bases, interpolation, and texture mapping. Each of these tasks involved its own individual challenges, and overall worked together to display complex images.

We began by implementing a naive algorithm to rasterize a triangle, in which we sample one point for each pixel in the framebuffer. While relatively fast and memory-efficient, this runs into some problems, particularly in high-frequency areas of our image, where we may run into jaggies and other aliasing artifacts.

To alleviate some of the artifacts, we implemented a supersampling algorithm which results in less aliasing at the expense of computation and memory.

With this, we are able to display triangles, and can deal with artifacts with higher sampling rates. However, we are still lacking a way to transform objects. Scaling, rotation, and translation (and their combinations) are all common transformations, and so we implemented these with matrices.

Next, we turned to barycentric coordinates as a way to easily interpolate between triangle vertices, particularly with colors, and would prove useful with the remaining task, texture mapping, where we used a change-of-basis into barycentric coordinates along with different pixel- and level-sampling methods to render textures.

Overall, we can now render, transform, and texture objects - enough for many graphics applications!
