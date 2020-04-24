# **Finding Lane Lines on the Road** 

## Writeup

### This writeup documents the approach and outcome of the findinng lane lines on the road project.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image_out]: ./test_images_output/solidWhiteCurve.jpg "Output"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I applied gaussian blur with the kernel size of 5. And after that Canny transform to get the edges. With the resulted image, I applied an image mask to focus on the region of interest. I selected the below half area of the image with some offset, because thats where the lane lines are located. Then I applied Hough transform to get the straight lines on the lanes. Finally I applied weight on the resultant image and the original image to get the final output image.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function first by getting the slopes of the lines and splitting them based on the positive and negative values to collect them in the corresponding left and right lines list. And then extrapolate those lines by using [cv2.fitLine](https://docs.opencv.org/2.4/modules/imgproc/doc/structural_analysis_and_shape_descriptors.html?highlight=fitline#cv2.fitLine) function.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![solidWhiteCurve.jpg][image_out]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when lane lines are very curvy on the turns. In which case the minimum line length used is bigger than the actual and thus fails to detect them.

Another shortcoming could be that having some vehicles on the lane before us thus hiding the parts of the lane, which might impact the proper working of our pipeline.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to automate the calibration of the parameters used for cv2 functions to find the optimal values.

Another potential improvement could be to use more test images and videos to find the corner cases and make our solution robust enough to handle such cases.

