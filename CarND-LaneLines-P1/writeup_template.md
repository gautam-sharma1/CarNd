# **Finding Lane Lines on the Road** 

## Writeup Template

### You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./img1.jpg "Grayscale"
[image2]: ./img2.jpg "Grayscale"
[image3]: ./img3.jpg "Grayscale"
[image4]: ./img4.jpg "Grayscale"
[image5]: ./img5.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale using cv2.cvtColor(image,cv2.COLOR_RGB2GRAY) command. Then I added a gaussian blur to the grayscale image. Following that I initialized a Canny edge detector with threshold[90,150].The canny detector returned edges on which I initalized a mask with zeros. After that I called the region_of_interest function with a polygon with 4 edges and got the mask edges as output which was then passed on to the hough_lines function.

I modified draw_lines() function by seperating the lines on the basis of slope. Then I took an average of the lines with positive slope and similarly with negative slope and the passed the result to the cv2.line() function.




### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be that it does not work properly on roads with curvature. It only works with staright markings on the road.




### 3. Suggest possible improvements to your pipeline

A possible improvement would be to calibrate the camera and then undistort the image and then do the same process as above. 
