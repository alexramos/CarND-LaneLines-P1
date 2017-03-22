# **Finding Lane Lines on the Road** 

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./test_images_output/solidWhiteRight_alg.png "Alg"
[image2]: ./test_images_output/solidWhiteRight_lines.jpg "Lanes"
[image3]: ./test_images_output/solidWhiteRight_lines_V2.jpg "Lanes_V2"

---

## Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consists of 6 steps. 

1. Convert image to grayscale to reduce noise in image.
2. Perform Gaussian kernel smoothing.
3. Find edges with Canny edge detector.
4. Mask image to only region of interest (trapezoidal area in front of car).
5. Detect line segments with Hough transform.
6. Overlay detected lines onto original image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function to first only consider detected line segments within a range of allowable slopes.  This prevents the slope of the final two output lines from being influenced by line segments that are too shallow or too steep to be real lane lines.  I then use a line segment's image position and slope to determine if it is part of either the left or right lane.  All valid left/right line segments coordinates are then averaged to derive two linear equations, one each for left and right lines.  Lastly, I extrapolate two lines spanning the bottom and top of my region-of-interest.

The figures below show how the pipeline works.

#### Pipeline steps 1-4 ran on solidWhiteRight.jpg.
![alt text][image1]

#### Pipeline steps 5-6.
![alt text][image2]

#### Pipeline steps 5-6 after modifying draw_lines() as described above.
![alt text][image3]

### 2. Identify potential shortcomings with your current pipeline

There are several shortcomings with the current lane-finding pipeline

- In the submitted output videos, the detected lines jitter a lot frame-to-frame.

- In the challenge video, my algorithm has a hard time detecting line segments from the left yellow line during the lighter asphalt portion of the video.

- I had to tweak the pipeline parameters in order to get it to work OK for the challenge video.  No single set of parameters  worked well for both the test images/videos and challenge video.

- The region-of-interest is hardcoded to a trapezoidal area that extends all the way to the bottom of an image.  If a large portion of the car (or another car) is in the image, many false line segments may be detected.

- The algorithm is only capable of drawing straight lines.  During sharp turns, the drawn lines will not reflect the actual curved path of lane lines in front of the car. 

### 3. Suggest possible improvements to your pipeline

A possible improvement would be to incorporate some notion of memory or history from previously detected lanes.  When processing video, N previous detected lines could be used to influence the current image's drawn lines.  For example, we could use an average of lines from a buffer.  This would make the drawn lines on a video appear smoother (less frame-to-frame jitter) and more robost to noise from a single frame.

Another potential improvement could be to incorporate color detection in our line finding algorithm.  This would help detect lines in cases where the algorithm performs poorly, notably yellow lines on lighter-colored asphalt.
