# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale, then I blurred the image and applied canny edge detection to the result.
I then masked the result of the canny edge detection using an area_of_interest from two points along the bottom of the image just in from the left and right edges and the apexes just below the center of the image to the left and right as the mask.
Finally, I applied a hough transform to the masked image. 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by checking the slopes of the lines and keeping lines on the left with negative slopes between -1.5 and -0.5, and the ones on the right with positive slopes between 0.5 and 1.5.
To average the lines, I stored distance calculations for each of the endpoints of the lines and found the points closest to the middle of the image and closest to the corner on the left and right sides.
These points where then extrapolated from the top of the area of interest to the bottom of the image.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![Before](/test_images/solidWhiteCurve.jpg)
![After](/test_images_output/solidWhiteCurve.jpg)

![Before](/test_images/solidWhiteRight.jpg)
![After](/test_images_output/solidWhiteRight.jpg)

![Before](/test_images/solidYellowCurve.jpg)
![After](/test_images_output/solidYellowCurve.jpg)

![Before](/test_images/solidYellowCurve2.jpg)
![After](/test_images_output/solidYellowCurve2.jpg)

![Before](/test_images/solidYellowLeft.jpg)
![After](/test_images_output/solidYellowLeft.jpg)

![Before](/test_images/whiteCarLaneSwitch.jpg)
![After](/test_images_output/whiteCarLaneSwitch.jpg)

### 2. Identify potential shortcomings with your current pipeline


The averaging method I used does not handle shadows across the road or other markings that could be confused with the lane markings.
Markings from tighter corners also are not handled well.

Another shortcoming is that the top of the area of interest is fixed, which creates problems on hilly terrain where the road drops down more abruptly.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to change the averaging method to ignore lines with outlying slopes and calculate an average slope on the remainder instead of simply finding min/max points. 

Another potential improvement could be to use the hough transform to identify the horizon and make the area of interest dynamic instead of static.
