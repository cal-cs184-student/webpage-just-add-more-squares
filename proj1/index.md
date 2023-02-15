---
layout: default
title: "Project 1: Rasterizer"
has_children: false
nav_order: 1
mathjax: true
---

![Lion](img/lion.png)

# Overview

For this project, we explored many fundamental ideas in computer graphics,
including rasterization, transformations, barycentric coordinates,
change-of-bases, interpolation, and texture mapping. Each of these tasks
involved its own individual challenges, and overall worked together to display
complex images.

We began by implementing a naive algorithm to rasterize a triangle, in which we
sample one point for each pixel in the framebuffer. While relatively fast and
memory-efficient, this runs into some problems, particularly in high-frequency
areas of our image, where we may run into jaggies and other aliasing artifacts.

To alleviate some of the artifacts, we implemented a supersampling algorithm
which results in less aliasing at the expense of computation and memory.

With this, we are able to display triangles, and can deal with artifacts with
higher sampling rates. However, we are still lacking a way to transform objects.
Scaling, rotation, and translation (and their combinations) are all common
transformations, and so we implemented these with matrices.

Next, we turned to barycentric coordinates as a way to easily interpolate
between triangle vertices, particularly with colors, and would prove useful with
the remaining task, texture mapping, where we used a change-of-basis into
barycentric coordinates along with different pixel- and level-sampling methods
to render textures.

We learned a lot about how graphics are rendered, transformed, and used in
conjunction with textures to build an image. There is so much more to be
explored here, particularly with implementation details for optimizing both
speed and quality, and we were captivated by how rich this topic can be. Some
interesting thoughts and challenges we had over the course of the project
include: 
- Averaging each pixel on-the-fly and then writing to the sample buffer without
having to store each supersample
- Numerical precision cascading errors with repeated operations on
floating-point numbers
- Implicit matrix-vector solutions and tradeoffs with regards to speed and
accuracy, especially near polygon edges
- Jittering points close to triangle edges may result in them being on the
outside of both triangles

Overall, this project was instrumental in learning the fundamentals of
rendering. We can now rasterize, transform, and texture objects - enough for
many graphics applications!


# Task 1

### Walk through how you rasterize triangles in your own words.

Unfortunately, we usually don’t have infinite precision on our displays, so
we need to have some way of translating infinitely-detailed triangles to
discrete pixels. To do this, we will choose the midpoint of each pixel in
the triangle and check if it falls inside the triangle. This involves, for
each edge of the triangle, determining whether the point falls inside or
outside that edge. If the point is on the same side of all three edges (all
inside), then we conclude that the point is inside the triangle. For points
directly on the edge, we chose to not implement the OpenGL rules, but
instead included them no matter which side of the triangle they reside.

### Explain how your algorithm is no worse than one that checks each sample within the bounding box of the triangle.

Our algorithm determines the minimum and maximum x- and y-values of the
triangle’s vertices, and uses these to form a bounding rectangle around the
triangle. We then step from the minimum to the maximum values to sample each
point and color it if inside the triangle, but ignore it if outside. This is
precisely the algorithm that checks each sample within the bounding box of
the triangle, so it is no worse than that one.

Here is the output of `basic/test4.svg` with a sample rate of 1 (i.e. no
supersampling). We can see that there is significant aliasing, particularly
because our sample rate isn't high enough to capture the thin corner of the
triangle. This leads us to the supersampling algorithm described in the
following task.

![test4-task1](img/basic-test4-rate-1.png)


# Task 2

To supersample with a given sample_rate, we calculated (sample_rate) equally
spaced points for a given pixel by calculating a step equal to
(sample_rate)^-0.5 then offsetting our minimum x- and y-values by one-half times
the step. From here, we step sqrt(sample_rate) - 1 steps in both the x- and y-
directions to effectively “grid” the given pixel with (sample_rate) equally
spaced points.

Each of these points represents one sample. Because we now have many more sample
points than pixels, we resized the sample_buffer to be sample_rate times its
original size and expanded the original flattened pixel cell within the
sample_buffer to sample_rate different cells.

Then, we sampled each of these points individually, and, depending on whether
they were inside or outside the triangle, wrote the given cell to the
corresponding cell in the now-expanded sample_buffer. Finally, in
resolve_to_framebuffer, we collapsed the value of these supersampled points by
taking the supersampled points’ average for a certain pixel and writing that
value into the frame_buffer.

Supersampling can be useful for reducing aliasing, because more samples means
that our Nyquist frequency is lower, and hence the algorithm develops an
increased resilience to fast changes in frequency. However, this comes at the
cost of both computational runtime and memory, because we have to both compute
and store sample_rate times more points.

Here is the output of `basic/test4.svg` with sample rates of 1, 4, and 16:

![test4-rate-1](img/basic-test4-rate-1.png)
![test4-rate-4](img/basic-test4-rate-4.png)
![test4-rate-16](img/basic-test4-rate-16.png)

We can see lots of aliasing with a sample rate of 1, significantly less with 4,
and much less with 16. This occurs because this portion of the image is “high
frequency” - at the corner of this very skinny triangle, we have a very sharp
change in color. This means that higher sample rates are able to capture this
change more accurately, and hence we see less aliasing.

# Task 3

![tree-pose-guy](img/tree-pose-guy.png)

This is tree pose guy. He do tree pose. To accomplish this, we had to modify the rotation of both arms and the left leg as well as scale some of the body parts up in length.

# Task 4

