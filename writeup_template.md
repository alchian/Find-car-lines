# **Finding Lane Lines on the Road** 

## Report

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./Find-car-lines/solidWhiteCurve.jpg "Grayscale"

---

### Reflection

![Alt text](Find-car-lines/solidWhiteCurve.jpg "optional title")

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

1st, I converted the images to grayscale;

2ed, I smoothed the gray image;

3rd, I find the edge use;

4th, I defined an area of interest to deal with, and to cut out the interst i don't care too much.

5th, I use cv2.HoughLinesP to find the lines in the same line

6th, 


In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
