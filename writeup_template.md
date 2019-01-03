# **Finding Lane Lines on the Road** 

## Report

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report

---

### Reflection



### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

I will describe my work step by step with the image given as "solidWhiteCurve.jpg":

![solidWhiteCurve.jpg](https://github.com/alchian/Find-car-lines/blob/test_images/solidWhiteCurve.jpg "solidWhiteCurve.jpg")

Step 1, I converted the images to grayscale with the function cv2.COLOR_RGB2GRAY;

![solidWhiteCurve_gray.jpg](https://github.com/alchian/Find-car-lines/blob/test_images/solidWhiteCurve_test_images_grayt.jpg "solidWhiteCurve_gray.jpg")

Step 2,  I smoothed the gray image with the function cv2.GaussianBlur to remove the noise point;

![solidWhiteCurve_smoothing.jpg](https://github.com/alchian/Find-car-lines/blob/test_images/solidWhiteCurve_test_images_smoothing.jpg "solidWhiteCurve_smoothing.jpg")

3rd, I find the edges of the smoothed gray image using function cv2.Canny;

![solidWhiteCurve_edges.jpg](https://github.com/alchian/Find-car-lines/blob/test_images/solidWhiteCurve_test_images_edges.jpg "solidWhiteCurve_edges.jpg")

4th, I defined an area of interest to deal with, and to cut out the interst i don't care too much. 

The region I tested ok here is dined with 4 points: [[(150,the botom of the image),(460, 320), (490, 320), (920,the botom of the image)]]

"Tesd ok" means the region either not contain too much ,nor cut off the information which is useful as the information of car lines. 

The function used here include np.zeros_like,  cv2.fillPoly, &cv2.bitwise_and. np.zeros_like is used here to create a zero image.cv2.fillPoly is used here to fill color.and cv2.bitwise_and is use here to add two images pixels by pixels.

![solidWhiteCurve_region_of_interest.jpg](https://github.com/alchian/Find-car-lines/blob/test_images/solidWhiteCurve_region_of_interest.jpg "solidWhiteCurve_region_of_interest.jpg")

5th, I use cv2.HoughLinesP to find the lines in the same line. 

The Minimum number of pixels making up a line here is 20.&Maximum gap in pixels between connectable line segments is 60. and draw the lines we find on the image ,we get the line image.

![solidWhiteCurve_line_image.jpg](https://github.com/alchian/Find-car-lines/blob/test_images/solidWhiteCurve_line_image.jpg "solidWhiteCurve_line_image.jpg")

6th, I add the line image to the intial iamge we deal with using funtion cv2.addWeight. I get the result as darw the line on the view image.

![solidWhiteCurve_drawline.jpg](https://github.com/alchian/Find-car-lines/blob/test_images/solidWhiteCurve_drawline.jpg "solidWhiteCurve_drwline.jpg")

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by codes like this, and get the image.

    
    for line in lines:
        for x1,y1,x2,y2 in line:
            s=(y2-y1)/(x2-x1)  #deine s as slopes of lines
            if s < 0: #judge the lines belong to left lane or right lane through s
                lines_left[n_left]=line
                slope_left = (slope_left*n_left + s)/(n_left+1) #cacualte the mean slope of the left lane
                n_left=n_left+1
                if y2< yminleft:
                    yminleft=y2 #find the farthest point of the left lane
                    xmaxleft=x2 
                    xminleft=int(xmaxleft-(yminleft-ymaxleft)/slope_left) #cacualte the mean slope of the left lane
            else:
                lines_right[n_right]=line
                slope_right = (slope_right*n_right + s)/(n_right+1)
                n_right=n_right+1
                if y1< yminright:
                    yminright=y1  
                    xminright=x1
                    xmaxright=int(xminright+(ymaxright-yminright)/slope_right)


![solidWhiteCurve_drawline.jpg](https://github.com/alchian/Find-car-lines/blob/test_images/solidWhiteCurve_single_line_image.jpg "solidWhiteCurve_drwline.jpg")

![solidWhiteCurve_single_line_image.jpg](https://github.com/alchian/Find-car-lines/blob/test_images/solidWhiteCurve_single_line_image.jpg"solidWhiteCurve_single_line_image.jpg")

### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...
