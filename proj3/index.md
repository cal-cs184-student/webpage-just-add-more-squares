---
layout: default
title: "Project 3: Path Tracer"
has_children: false
nav_order: 1
mathjax: true
---

![bunny bunny bunny](./img/bunny-main.png){:style="display:block; margin-left: auto; margin-right: auto; width:70%;"}

## Overview

YOUR RESPONSE GOES HERE

<br>

## Part 1: Ray Generation and Scene Intersection (20 Points)

<!-- Walk through the ray generation and primitive intersection parts of the rendering pipeline. -->

During ray generation, we take a coordinate in the image and create a corresponding ray in the world space. 

The first step involves taking a normalized image coordinate ($(x, y)$ where $w, y \in [0, 1]$) and converting it to the camera space. Specifically, the camera space assumes there's a sensor at $z = -1$ and has corners at $(-\tan(\frac{\text{hFov}}{2}), -\tan(\frac{\text{vFov}}{2}), -1)$ and $(\tan(\frac{\text{hFov}}{2}), \tan(\frac{\text{vFov}}{2}), -1)$. By taking $(x, y)$ and linearly interpolating along the axes of the rectangles, we get the camera space coordinates.

$x_C = (1 - x) \cdot -\tan(\frac{\text{hFov}}{2}) + x \cdot \tan(\frac{\text{hFov}}{2})$

$y_C = (1 - y) \cdot -\tan(\frac{\text{vFov}}{2}) + y \cdot \tan(\frac{\text{vFov}}{2})$

$z_C = -1$

Then, to get a ray in the world space, we set the origin of the ray to the camera's position and we multiply the camera-space vector by our camera-to-world coordinate transform matrix `c2w`.

Now that we are able to generate a ray given a coordinate in the image space, we utilized it to sample pixels of the image. In each pixel, we use a sampler to choose points within the pixel. For each point, we generate a ray that goes through it and compute the average radiance along all our sampled rays. We accumulate this information in our sample buffer.

To sample along each ray direction, we also need to know where our ray intersects different objects (primitives) inside of our world. During this part of the project, we implemented intersections for both triangles and spheres. Overall, the process involves first running a primitive-ray intersection test, then setting variables like the normal direction, distance until intersection, BSDF at the intersection point, and so on.

<!-- Explain the triangle intersection algorithm you implemented in your own words. -->

For example, with triangle intersection, we compute the intersection point using the [Moller-Trumbore algorithm](https://cs184.eecs.berkeley.edu/sp23/lecture/9-22/intro-to-ray-tracing-and-acceler). This algorithm solves for $t, b_1, b_2$ where $t$ is the ray parameter and $b_1, b_2$ are two of the barycentric coordinates of the triangle we're checking intersection with.

In order to be an intersection, `t` must be between the ray's `min_t` and `max_t` variables and the barycentric coordinates must be non-negative.

Additionally, upon intersection, we need to update some of the variables in `isect`. Specifically, we want to update the ray's `max_t` to `t` because we don't want to consider intersections behind the one we just found. We also want to use the barycentric coordinates to interpolate the normal direction using the normals at the vertices. Finally, we want to set the primitive and it's corresponding BSDF.

<!-- Show images with normal shading for a few small .dae files. -->

| **CBspheres.dae** | **CBcoil.dae** |
|:---:|:---:|
| ![CBspheres](./img/part-1/CBspheres.png) | ![CBcoil](./img/part-1/CBcoil.png) |
| **cow.dae** | **bench.dae** |
| ![cow](./img/part-1/cow.png) | ![bench](./img/part-1/bench.png) |

## Part 2: Bounding Volume Hierarchy (20 Points)

### Walk through your BVH construction algorithm. Explain the heuristic you chose for picking the splitting point.

Our BVH construction algorithm recursively creates the BVH nodes by splitting at the median centroid along the longest axis and terminating when there are fewer than `max_leaf_size` primitives left.

First, we compute the bounding box `bbox` of all primitives in the node by looping through the node and expanding by the primitive's bounding box. Using this bounding box, we create a new BVH node.

If the BVH node we created contains fewer than `max_leaf_size` primitives, it will be a leaf node with all of the primitives.

Otherwise, we must split the BVH node further. In order to do so, we use the `extent` variable and find the longest axis of the bounding box. Then, we sort the primitives from `start` to `end`, ordered by their centroid's position along this axis. This sorting is in-place and we never need to create more vectors to hold primitives. We then take the median centroid `mid` to split on using pointer arithmetic and recursively construct the left and right BVH nodes with all the primitives from `start` to `mid` and `mid` to `end`, respectively. Because we're using the median in this manner, there will always be non-empty collections of primitives on each side of the split.

### Show images with normal shading for a few large .dae files that you can only render with BVH acceleration.

<!-- Example of including multiple figures -->

| **CBlucy.dae** | **CBdragon.dae** |
|:---:|:---:|
| ![CBlucy](./img/part-2/lucy.png) | ![CBdragon](./img/part-2/CBdragon.png) |
| **blob.dae** | **wall-e.dae** |
| ![blob](./img/part-2/blob.png) | ![wall-e](./img/part-2/wall-e.png) |

### Compare rendering times on a few scenes with moderately complex geometries with and without BVH acceleration. Present your results in a one-paragraph analysis.

Our BVH acceleration resulted in speedup for most images, sometimes orders of magnitudes faster, when rendering images. As the number of primitives in the object increased, the speedup became more and more noticeable. However, if there were only a handful of primitives (like CBspheres), not using BVH was faster because there's less overhead. The results from a couple of these images are compiled below:

| Image | Rendering Time without BVH (s) | Rendering Time with BVH (s) |
|:---:|:---:|:---:|
| CBspheres | 0.0428 | 0.0502 |
| teapot | 2.4553 | 0.0572 |
| cow | 5.4124 | 0.0569 |
| bunny | 38.2385 | 0.0806 |


## Part 3: Direct Illumination (20 Points)

### Walk through both implementations of the direct lighting function.

YOUR RESPONSE GOES HERE

### Show some images rendered with both implementations of the direct lighting function.

<!-- Example of including multiple figures -->
<div align="middle">
  <table style="width:100%">
    <!-- Header -->
    <tr align="center">
      <th>
        <b>Uniform Hemisphere Sampling</b>
      </th>
      <th>
        <b>Light Sampling</b>
      </th>
    </tr>
    <br>
    <tr align="center">
      <td>
        <img src="images/your_file.png" align="middle" width="400px"/>
        <figcaption>example1.dae</figcaption>
      </td>
      <td>
        <img src="images/your_file.png" align="middle" width="400px"/>
        <figcaption>example1.dae</figcaption>
      </td>
    </tr>
    <br>
    <tr align="center">
      <td>
        <img src="images/your_file.png" align="middle" width="400px"/>
        <figcaption>example2.dae</figcaption>
      </td>
      <td>
        <img src="images/your_file.png" align="middle" width="400px"/>
        <figcaption>example2.dae</figcaption>
      </td>
    </tr>
    <br>
  </table>
</div>
<br>

### Focus on one particular scene with at least one area light and compare the noise levels in soft shadows when rendering with 1, 4, 16, and 64 light rays (the -l flag) and with 1 sample per pixel (the -s flag) using light sampling, not uniform hemisphere sampling.

| Number of Light Rays | `CBbunny.dae` |
|:---:|:---:|
| 1 | ![CBbunny 1 Ray](./img/part-3/bunny-l-1.png) |
| 4 | ![CBbunny 4 Rays](./img/part-3/bunny-l-4.png) |
| 16 | ![CBbunny 16 Rays](./img/part-3/bunny-l-16.png) |
| 64 | ![CBbunny 64 Rays](./img/part-3/bunny-l-64.png) |

When sampling with more light rays, the shadow of the bunny becomes significantly softer, even with just one sample per pixel. This is because we are using importance sampling, so having more samples per light source has a smoothing effect for pixels that are on the edges of shadows, due to the fact that sometimes they will hit a point on the light and other times be obstructed. When we have more light rays, we can average this effect, so the shadows will become softer.

### Compare the results between uniform hemisphere sampling and lighting sampling in a one-paragraph analysis.

YOUR RESPONSE GOES HERE


## Part 4: Global Illumination (20 Points)

### Walk through your implementation of the indirect lighting function.

YOUR RESPONSE GOES HERE

### Show some images rendered with global (direct and indirect) illumination. Use 1024 samples per pixel.

<!-- Example of including multiple figures -->
<div align="middle">
  <table style="width:100%">
    <tr align="center">
      <td>
        <img src="images/your_file.png" align="middle" width="400px"/>
        <figcaption>example1.dae</figcaption>
      </td>
      <td>
        <img src="images/your_file.png" align="middle" width="400px"/>
        <figcaption>example2.dae</figcaption>
      </td>
    </tr>
  </table>
</div>

### Pick one scene and compare rendered views first with only direct illumination, then only indirect illumination. Use 1024 samples per pixel. (You will have to edit PathTracer::at_least_one_bounce_radiance(...) in your code to generate these views.)

<!-- Example of including multiple figures -->
<div align="middle">
  <table style="width:100%">
    <tr align="center">
      <td>
        <img src="images/your_file.png" align="middle" width="400px"/>
        <figcaption>Only direct illumination (example1.dae)</figcaption>
      </td>
      <td>
        <img src="images/your_file.png" align="middle" width="400px"/>
        <figcaption>Only indirect illumination (example1.dae)</figcaption>
      </td>
    </tr>
  </table>
</div>

YOUR EXPLANATION GOES HERE


### For CBbunny.dae, compare rendered views with max_ray_depth set to 0, 1, 2, 3, and 100 (the -m flag). Use 1024 samples per pixel.

| `max_ray_depth` | `CBbunny.dae` render |
|:-------------:|:---:|
| 0 | ![Bunny-0](./img/part-4/bunny-0.png)  |
| 1 | ![Bunny-1](./img/part-4/bunny-1.png)  |
| 2 | ![Bunny-2](./img/part-4/bunny-2.png)  |
| 3 | ![Bunny-3](./img/part-4/bunny-3.png)  |
| 100 | ![Bunny-100](./img/part-4/bunny-100.png)  |


We generated each of these renders using Russian roulette with a termination probability of 0.3. As `max_ray_depth` increases, indirect lighting from reflections and bounces have more paths available to every single point. This means that the image will generally be brighter because there are more light "sources," (the reflections off non-light-source points) and we also will gain reflected colors (most easily seen in the slightly reddish-bluish ceiling of the 100-depth render). Also, the shadows become softer and are also tinted the color of the walls.

### Pick one scene and compare rendered views with various sample-per-pixel rates, including at least 1, 2, 4, 8, 16, 64, and 1024. Use 4 light rays.

| Sample Rate | `CBspheres.dae` render |
|:-------------:|:---:|
| 1 | ![Spheres-1](./img/part-4/spheres-1.png)  |
| 2 | ![Spheres-2](./img/part-4/spheres-2.png)  |
| 4 | ![Spheres-4](./img/part-4/spheres-4.png)  |
| 8 | ![Spheres-8](./img/part-4/spheres-8.png)  |
| 16 | ![Spheres-16](./img/part-4/spheres-16.png)  |
| 64 | ![Spheres-64](./img/part-4/spheres-64.png)  |
| 256 | ![Spheres-256](./img/part-4/spheres-256.png)  |
| 1024 | ![Spheres-1024](./img/part-4/spheres-1024.png)  |

For the above renders, we used 16 samples per area light, with a maximum ray depth of 1000. We can see that with more samples per pixel, the image gets significantly less noisy and appears slightly brighter.

<!-- TODO: Add reasoning why this is the case. -->

## Part 5: Adaptive Sampling (20 Points)

<!-- Explain adaptive sampling. Walk through your implementation of the adaptive sampling.
Pick one scene and render it with at least 2048 samples per pixel. Show a good sampling rate image with clearly visible differences in sampling rate over various regions and pixels. Include both your sample rate image, which shows your how your adaptive sampling changes depending on which part of the image you are rendering, and your noise-free rendered result. Use 1 sample per light and at least 5 for max ray depth. -->

### Explain adaptive sampling. Walk through your implementation of the adaptive sampling.

Adaptive sampling is where we sample high-frequency regions of the image more because lower-frequency regions do not require as many samples to become relatively noise-free. This is done by comparing the standard deviation of the samples for a pixel to a threshold value. If the threshold condition is met, more samples will likely not change the pixel's final value very much, so we can terminate computation early. If the threshold condition is not met, then we sample that pixel more to reduce the variance. We can also set a maximum number of samples per region to prevent pixels from being sampled too many times.

There is one subtle detail that makes this process difficult to implement in the code - we have three separate variances, for the R, G, and B channels in the image. We use the `illum` function of `Vector3D` to convert this to a single scalar value. From here, we accumulate the variables

$$\begin{align} s_1 &:= \sum_{i=1}^n \, \texttt{illum}(r_i) \\ s_2 &:= \sum_{i=1}^n \, \left(\texttt{illum}(r_i)\right)^2\end{align}$$

where $r_i$ is the estimated global illumination radiance of the $i$th sample. We then compute the desired statistics as

$$\begin{align} \mu &= \frac{s_1}{n} \\ \sigma^2 &= \frac{1}{n-1} \left(s_2 - \frac{s_1^2}{n}\right)\end{align}$$

where $\mu$ is the mean and $\sigma^2$ is the variance. The threshold condition is given by

$$ 1.96 \cdot \frac{\sigma}{\sqrt{n}} \leq \text{maxTolerance} \cdot \mu$$

If the statistics satisfy this condition, then no more sampling is done for that pixel. It would be unnecessarily costly to compute these statistics for every sample, so we instead check the stopping condition every `samplesPerBatch` samples.

This process speeds up the sampling process significantly while maintaining most of the quality, as shown in the following renders:

### Pick two scenes and render them with at least 2048 samples per pixel. Show a good sampling rate image with clearly visible differences in sampling rate over various regions and pixels. Include both your sample rate image, which shows your how your adaptive sampling changes depending on which part of the image you are rendering, and your noise-free rendered result. Use 1 sample per light and at least 5 for max ray depth.

We used a maximum tolerance of 0.05 for adaptive sampling, with 64 samples per batch, a sample rate of 2048, 1 sample per light, and a maximum ray depth of 5.

| Scene | Sample Rate Image | Rendered Image | Time to Render (s)
|:-------------:|:---:|:---:|:---:|
| `CBbunny.dae` (no adaptive) | ![bunny-no-adaptive-rate](./img/part-5/bunny-no-adaptive-rate.png)  | ![bunny-no-adaptive](./img/part-5/bunny-no-adaptive.png)  | 883 |
| `CBbunny.dae` (adaptive) | ![bunny-adaptive-rate](./img/part-5/bunny-adaptive-rate.png)  | ![bunny-adaptive](./img/part-5/bunny-adaptive.png)  | 651 |
| `wall-e.dae` (no adaptive) | ![wall-e-no-adaptive-rate](./img/part-5/wall-e-no-adaptive-rate.png)  | ![wall-e-no-adaptive](./img/part-5/wall-e-no-adaptive.png)  | 2157 |
| `wall-e.dae` (adaptive) | ![wall-e-adaptive-rate](./img/part-5/wall-e-adaptive-rate.png)  | ![wall-e-adaptive](./img/part-5/wall-e-adaptive.png)  | 1567 |

More-frequently-sampled regions are red, and less-frequently-sampled regions are blue. We can see that high-frequency (detailed) regions of the images are sampled more frequently and low-frequency (smooth) regions are sampled less frequently. This results in a significant speedup in rendering time while maintaining most of the quality.
