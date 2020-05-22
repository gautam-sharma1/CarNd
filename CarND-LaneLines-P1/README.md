# **Finding Lane Lines on the Road** 
[![Udacity - Self-Driving Car NanoDegree]

<img src="img1.png" width="480" alt="Combined Image" />
<img src="img2.png" width="480" alt="Combined Image" />
<img src="img3.png" width="480" alt="Combined Image" />
<img src="img4.png" width="480" alt="Combined Image" />
<img src="img5.png" width="480" alt="Combined Image" />
Overview
---

When we drive, we use our eyes to decide where to go.  The lines on the road that show us where the lanes are act as our constant reference for where to steer the vehicle.  Naturally, one of the first things we would like to do in developing a self-driving car is to automatically detect lane lines using an algorithm.

In this project you will detect lane lines in images using Python and OpenCV.  OpenCV means "Open-Source Computer Vision", which is a package that has many useful tools for analyzing images.  

To complete the project, two files will be submitted: a file containing project code and a file containing a brief write up explaining your solution. We have included template files to be used both for the [code](https://github.com/udacity/CarND-LaneLines-P1/blob/master/P1.ipynb) and the [writeup](https://github.com/udacity/CarND-LaneLines-P1/blob/master/writeup_template.md).The code file is called P1.ipynb and the writeup template is writeup_template.md 

To meet specifications in the project, take a look at the requirements in the [project rubric](https://review.udacity.com/#!/rubrics/322/view)


### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 5 steps. First, I converted the images to grayscale using cv2.cvtColor(image,cv2.COLOR_RGB2GRAY) command. Then I added a gaussian blur to the grayscale image. Following that I initialized a Canny edge detector with threshold[90,150].The canny detector returned edges on which I initalized a mask with zeros. After that I called the region_of_interest function with a polygon with 4 edges and got the mask edges as output which was then passed on to the hough_lines function.

I modified draw_lines() function by seperating the lines on the basis of slope. Then I took an average of the lines with positive slope and similarly with negative slope and the passed the result to the cv2.line() function.




### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be that it does not work properly on roads with curvature. It only works with staright markings on the road.




### 3. Suggest possible improvements to your pipeline

A possible improvement would be to calibrate the camera and then undistort the image and then do the same process as above. 
 


The Project
---

## If you have already installed the [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md) you should be good to go!   If not, you should install the starter kit to get started on this project. ##

**Step 1:** Set up the [CarND Term1 Starter Kit](https://classroom.udacity.com/nanodegrees/nd013/parts/fbf77062-5703-404e-b60c-95b78b2f3f9e/modules/83ec35ee-1e02-48a5-bdb7-d244bd47c2dc/lessons/8c82408b-a217-4d09-b81d-1bda4c6380ef/concepts/4f1870e0-3849-43e4-b670-12e6f2d4b7a7) if you haven't already.

**Step 2:** Open the code in a Jupyter Notebook

You will complete the project code in a Jupyter notebook.  If you are unfamiliar with Jupyter Notebooks, check out <A HREF="https://www.packtpub.com/books/content/basics-jupyter-notebook-and-python" target="_blank">Cyrille Rossant's Basics of Jupyter Notebook and Python</A> to get started.

Jupyter is an Ipython notebook where you can run blocks of code and see results interactively.  All the code for this project is contained in a Jupyter notebook. To start Jupyter in your browser, use terminal to navigate to your project directory and then run the following command at the terminal prompt (be sure you've activated your Python 3 carnd-term1 environment as described in the [CarND Term1 Starter Kit](https://github.com/udacity/CarND-Term1-Starter-Kit/blob/master/README.md) installation instructions!):

`> jupyter notebook`

A browser window will appear showing the contents of the current directory.  Click on the file called "P1.ipynb".  Another browser window will appear displaying the notebook.  Follow the instructions in the notebook to complete the project.  

## Authors

* **Gautam Sharma** - *Initial work* - [github](https://github.com/gautam-sharma1)



## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Udacity and the whole Self driving Car Nanodegree Team


