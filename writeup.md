# **Finding Lane Lines on the Road**

## Writeup
---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road using various different CV algorithms.

[//]: # (Image References)
[image1]: ./examples/grayscale.jpg "Grayscale"

[output_img_0]: ./test_images_output/solidWhiteCurve.jpg "Solid White Curve Output"
[output_img_1]: ./test_images_output/solidwhiteRight.jpg "Solid White Right Output"
[output_img_2]: ./test_images_output/solidYellowCurve.jpg "SYCJ"
[output_img_3]: ./test_images_output/solidYellowCurve2.jpg "SYCJ2"
[output_img_4]: ./test_images_output/solidYellowLeft.jpg "SYCJ3"
[output_img_5]: ./test_images_output/whiteCarLaneSwitch.jpg "SYCJ4"

[output_gif_0]: ./test_videos_output/gif/solidWhiteRight.gif "SWRG"
[output_gif_1]: ./test_videos_output/gif/solidYellowLeft.gif "SYLG"

---

### Reflection

### 1. Pipeline Process Description

The pipeline generated for this topic required the following steps.

- First up was preprocessing the image using  grayscale for Canny Edge Detection (CED). 

- Next, the Gaussian Blur algorithm was applied to reduce background noise, and hence lower the chance of picking up incorrect lines from CED. 

- CED was then used to detect the edges inside of the image. 

- After CED, region masking was applied to remove unneeded edges defined by the algorithm. The masking figure was defined by using a triangular shape, similar to that of the trajectory shape.

- Following the masking was the application of houghlines, an algorithm that allowed for the generation of lines based on line length, spacing and more. Those requirements were shuffled around until a decently shaped houghline formed as a result.

- Inside the houghlines function, the function drawlines is used, which applies the set of lines generated from the houghlines onto the picture. IMPORTANT! However, the draw lines function was edited such that an average of all the lines collected was drawn. This was done by separating both lines based on slope, and then averaging the lines on each side based on the starting and ending point.

- Finally, given the new lines drawn, an additional weight was added to both edges to draw a more filled line.

### Results

#### Given samples of photos with paths drawn onto them.

![alt text][output_img_0]
![alt text][output_img_1]
![alt text][output_img_2]
![alt text][output_img_3]
![alt text][output_img_4]
![alt text][output_img_5]

#### Given samples of videos with paths drawn onto them.

![alt text][output_gif_0]
![alt text][output_gif_1]


### 2. Potential Shortcomings of Pipeline

Unfortunately, in any real-world condition the ideal condition is seldom applicable. 

Following statements below show potential shortcomings:

- Tight corners will fail the region masking based on triangulation. 

- During night-time the level of noise reduction provided by the Gaussian Blur, and other thresholds in general will need to be reduced.

- Suppose there are cars in front of us such that the lanes are not completely visible.


### 3. Possible Pipeline Improvements

- Increase region visible or completely ignore the use of region masking since paths can differ in real world scenarios. Would require use of more complex noise reduction techniques.

- Path prediction based on previous paths.

- Use of other noise reduction techniques, esp. for merging differences between night and day path finding.

- Limit slope such that there exists a range, where small slopes get caught as errors and are ignored.
