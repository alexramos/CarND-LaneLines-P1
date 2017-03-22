# **Finding Lane Lines on the Road** 

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteCurve_alg.png "Alg"

---

## Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. 

1. Convert image to grayscale.
2. Perform Gaussian kernel smooth
3. Find edges with Canny edge detector
4. Mask image to only region of interest (trapezoidal area in front of car)
5. Detect line segments with Hough transform
6. Overlay detected lines onto original image

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

The figure below shows how the pipeline work.

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline

There are several shortcomings with the current lane-finding pipeline

- jittering
- yellow lines
- car in front

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
