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

### Walk through the ray generation and primitive intersection parts of the rendering pipeline.

YOUR RESPONSE GOES HERE

### Explain the triangle intersection algorithm you implemented in your own words.

YOUR RESPONSE GOES HERE

### Show images with normal shading for a few small .dae files.

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
    <tr align="center">
      <td>
        <img src="images/your_file.png" align="middle" width="400px"/>
        <figcaption>example3.dae</figcaption>
      </td>
      <td>
        <img src="images/your_file.png" align="middle" width="400px"/>
        <figcaption>example4.dae</figcaption>
      </td>
    </tr>
  </table>
</div>

## Part 2: Bounding Volume Hierarchy (20 Points)

### Walk through your BVH construction algorithm. Explain the heuristic you chose for picking the splitting point.

YOUR RESPONSE GOES HERE

### Show images with normal shading for a few large .dae files that you can only render with BVH acceleration.

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
    <tr align="center">
      <td>
        <img src="images/your_file.png" align="middle" width="400px"/>
        <figcaption>example3.dae</figcaption>
      </td>
      <td>
        <img src="images/your_file.png" align="middle" width="400px"/>
        <figcaption>example4.dae</figcaption>
      </td>
    </tr>
  </table>
</div>

### Compare rendering times on a few scenes with moderately complex geometries with and without BVH acceleration. Present your results in a one-paragraph analysis.

YOUR RESPONSE GOES HERE

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

<!-- Example of including multiple figures -->
<div align="middle">
  <table style="width:100%">
    <tr align="center">
      <td>
        <img src="images/your_file.png" align="middle" width="200px"/>
        <figcaption>1 Light Ray (example1.dae)</figcaption>
      </td>
      <td>
        <img src="images/your_file.png" align="middle" width="200px"/>
        <figcaption>4 Light Rays (example1.dae)</figcaption>
      </td>
    </tr>
    <tr align="center">
      <td>
        <img src="images/your_file.png" align="middle" width="200px"/>
        <figcaption>16 Light Rays (example1.dae)</figcaption>
      </td>
      <td>
        <img src="images/your_file.png" align="middle" width="200px"/>
        <figcaption>64 Light Rays (example1.dae)</figcaption>
      </td>
    </tr>
  </table>
</div>

YOUR EXPLANATION GOES HERE

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

| `max_ray_depth` | result |
|:-------------:|:---:|
| 0 | ![Bunny-0](./img/bunny-0.png)  |
| 1 | ![Bunny-1](./img/bunny-1.png)  |
| 2 | ![Bunny-2](./img/bunny-2.png)  |
| 3 | ![Bunny-3](./img/bunny-3.png)  |
| 100 | ![Bunny-100](./img/bunny-100.png)  |


YOUR EXPLANATION GOES HERE


### Pick one scene and compare rendered views with various sample-per-pixel rates, including at least 1, 2, 4, 8, 16, 64, and 1024. Use 4 light rays.


<!-- Example of including multiple figures -->
<div align="middle">
  <table style="width:100%">
    <tr align="center">
      <td>
        <img src="images/your_file.png" align="middle" width="400px"/>
        <figcaption>max_ray_depth = 0 (CBbunny.dae)</figcaption>
      </td>
      <td>
        <img src="images/your_file.png" align="middle" width="400px"/>
        <figcaption>max_ray_depth = 1 (CBbunny.dae)</figcaption>
      </td>
    </tr>
    <tr align="center">
      <td>
        <img src="images/your_file.png" align="middle" width="400px"/>
        <figcaption>max_ray_depth = 2 (CBbunny.dae)</figcaption>
      </td>
      <td>
        <img src="images/your_file.png" align="middle" width="400px"/>
        <figcaption>max_ray_depth = 3 (CBbunny.dae)</figcaption>
      </td>
    </tr>
    <tr align="center">
      <td>
        <img src="images/your_file.png" align="middle" width="400px"/>
        <figcaption>max_ray_depth = 100 (CBbunny.dae)</figcaption>
      </td>
    </tr>
  </table>
</div>

YOUR EXPLANATION GOES HERE


## Part 5: Adaptive Sampling (20 Points)

<!-- Explain adaptive sampling. Walk through your implementation of the adaptive sampling.
Pick one scene and render it with at least 2048 samples per pixel. Show a good sampling rate image with clearly visible differences in sampling rate over various regions and pixels. Include both your sample rate image, which shows your how your adaptive sampling changes depending on which part of the image you are rendering, and your noise-free rendered result. Use 1 sample per light and at least 5 for max ray depth. -->

### Explain adaptive sampling. Walk through your implementation of the adaptive sampling.

Adaptive sampling is where we sample high-frequency regions of the image more because lower-frequency regions do not require as many samples to become relatively noise-free. This is done by comparing the variance of the samples in a region to a threshold value. If the variance is below the threshold, then we do not need to sample that region more. If the variance is above the threshold, then we sample that region more to reduce the variance. We can also use a maximum number of samples per region to prevent regions from being sampled too many times.

There is one subtle detail that makes this process difficult to implement in the code - we have three separate variances, for the R, G, and B channels in the image. We use the `illum` function of `Vector3D` to map this to a single scalar value. From here, we accumulate the variables

$$\begin{align} s_1 &:= \sum_{i=1}^n \texttt{illum}(r_i) \\ s_2 &:= \sum_{i=1}^n (\texttt{illum}(r_i))^2\end{align}$$

where $r_i$ is the estimated global illumination radiance of the $i$th sample. We then compute the desired statistics as

$$\begin{align} \mu &:= \frac{s_1}{n} \\ \sigma^2 &:= \frac{1}{n-1} \left(s_2 - \frac{s_1^2}{n}\right)\end{align}$$

where $\mu$ is the mean and $\sigma^2$ is the variance. The stopping condition is given by

$$ 1.96 \cdot \frac{\sigma}{\sqrt{n}} \leq \text{maxTolerance} \cdot \mu$$

If the statistics satisfy this condition, then no more sampling is done for that pixel. It would be unnecessarily costly to compute these statistics for every sample, so we instead check the stopping condition every `samplesPerBatch` samples.

This process speeds up the sampling process significantly while maintaining most of the quality, as shown in the following renders:

### Pick two scenes and render them with at least 2048 samples per pixel. Show a good sampling rate image with clearly visible differences in sampling rate over various regions and pixels. Include both your sample rate image, which shows your how your adaptive sampling changes depending on which part of the image you are rendering, and your noise-free rendered result. Use 1 sample per light and at least 5 for max ray depth.

We used a maximum tolerance of 0.05 for adaptive sampling, with 64 samples per batch, a sample rate of 2048, 1 sample per light, and a max ray depth of 5.

| Scene | Sample Rate Image | Rendered Image | Time to Render (s)
|:-------------:|:---:|:---:|:---:|
| `CBbunny.dae` (no adaptive) | ![bunny-no-adaptive-rate](./img/bunny-no-adaptive-rate.png)  | ![bunny-no-adaptive](./img/bunny-no-adaptive.png)  | |
| `CBbunny.dae` (adaptive) | ![bunny-adaptive-rate](./img/bunny-adaptive-rate.png)  | ![bunny-adaptive](./img/bunny-adaptive.png)  | |
| `wall-e.dae` (no adaptive) | ![wall-e-no-adaptive-rate](./img/wall-e-no-adaptive-rate.png)  | ![wall-e-no-adaptive](./img/wall-e-no-adaptive.png)  | 2157 |
| `wall-e.dae` (adaptive) | ![wall-e-adaptive-rate](./img/wall-e-adaptive-rate.png)  | ![wall-e-adaptive](./img/wall-e-adaptive.png)  | 1567 |
