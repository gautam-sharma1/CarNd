# **Traffic Sign Recognition** 

## Writeup
---

**Build a Traffic Sign Recognition Project**

The goals / steps of this project are the following:
* Load the data set (see below for links to the project data set)
* Explore, summarize and visualize the data set
* Design, train and test a model architecture
* Use the model to make predictions on new images
* Analyze the softmax probabilities of the new images
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./examples/visualization.jpg "Visualization"
[image2]: ./examples/grayscale.jpg "Grayscaling"
[image3]: ./examples/random_noise.jpg "Random Noise"
[image4]: ./examples/placeholder.png "Traffic Sign 1"
[image5]: ./examples/placeholder.png "Traffic Sign 2"
[image6]: ./examples/placeholder.png "Traffic Sign 3"
[image7]: ./examples/placeholder.png "Traffic Sign 4"
[image8]: ./examples/placeholder.png "Traffic Sign 5"

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/481/view) individually and describe how I addressed each point in my implementation.  

---
### Writeup / README

#### 1. Provide a Writeup / README that includes all the rubric points and how you addressed each one. You can submit your writeup as markdown or pdf. You can use this template as a guide for writing the report. The submission includes the project code.

You're reading it! and here is a link to my [project code](https://github.com/gautam-sharma1/CarNd/tree/master/CarND-Traffic-Sign-Classifier-Project

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799
* The size of the validation set is 12630
* The size of test set is 4410
* The shape of a traffic sign image is 32X32X3
* The number of unique classes/labels in the data set is 43

#### 2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showinng the number of input images corresponding to their labels.

![alt text](bar.png)

### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

As a first step, I decided to convert the images to grayscale because it helps flatten the input width and also preserves key features.

Here is an example of a traffic sign image before grayscaling.

![alt text](original.png)

As a last step, I normalized the image data because it helps in making the bias and variance close to zero.

Here is an example of an original image and an augmented image:

![alt text](before.png)



#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x1 RGB image   							| 
| Convolution 5x5     	| 1x1 stride, same padding, outputs 28x28x6 	|
| RELU					|												|
| Convolution 5x5      	| 1x1 stride, same padding, outputs 14x14x10 			|
| RELU					|												|
| Convolution 5x5   	| 1x1 stride, same padding, outputs 8x8x16 			|
| RELU					|												|
| Max Pool		2x2		|		2x2 stride, outputs 4x4x16										|
| Fully connected		|Input = 256, Output = 120       									|
| RELU					|												|
| Dropout				|	keep_prob = 0.5											|
| Fully connected		|Input = 120, Output = 100     									|
| RELU					|												|
| Fully connected		|Input = 100, Output = 84     									|
| RELU					|												|      									|
| Fully connected		|Input = 84, Output = 43     									|
| Softmax				| 43 classes



#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used a learning rate of 0.001 with 10 EPOCHS and a Batch Size of 128. I also used Adam Optimizer as it tends to perform better than SGD.

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 94.3
* validation set accuracy of 96.2
* test set accuracy of 80

I used an iterative approach for the optimization of validation accuracy:

As an initial model architecture the original LeNet model from the course was chosen. In order to tailor the architecture for the traffic sign classifier usecase I adapted the input so that it accepts the colow images from the training set with shape (32,32,3) and I modified the number of outputs so that it fits to the 43 unique labels in the training set. The training accuracy was 83.5% and my test traffic sign "pedestrians" was not correctly classified. (used hyper parameters: EPOCHS=10, BATCH_SIZE=128, learning_rate = 0,001, mu = 0, sigma = 0.1)

After adding the grayscaling preprocessing the validation accuracy increased to 91% (hyperparameter unmodified)

The additional normalization of the training and validation data resulted in a minor increase of validation accuracy: 91.8% (hyperparameter unmodified)

reduced learning rate and increased number of epochs. validation accuracy = 93% (EPOCHS = 30, BATCH_SIZE = 128, rate = 0.0007, mu = 0, sigma = 0.1)

overfitting. added dropout layer after relu of final fully connected layer: validation accuracy = 94,7% (EPOCHS = 30, BATCH_SIZE = 128, rate = 0,0007, mu = 0, sigma = 0.1)

still overfitting. added dropout after relu of first fully connected layer. Overfitting reduced but still not good

added dropout before validation accuracy = 0.953 validation accuracy = 92% (EPOCHS = 50, BATCH_SIZE = 128, rate = 0,0007, mu = 0, sigma = 0.1)

further reduction of learning rate and increase of epochs. validation accuracy = 95.2% (EPOCHS = 150, BATCH_SIZE = 128, rate = 0,0006, mu = 0, sigma = 0.1)

### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are five German traffic signs that I found on the web:

![alt text](p1.png)![alt text](p2.png)![alt text](p3.png)
![alt text](p4.png) ![alt text](p5.png)


#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| Wild Animals      		| Wild Animals   									| 
| Pedestrian     			| Pedestrian 										|
| Ahead Only				| Slippery Road 										|
| Bicycle	      		|Children Crossing	 				 				|
| No entry			|    No entry  							|


The model was able to correctly guess 4 of the 5 traffic signs, which gives an accuracy of 80%. This compares favorably to the accuracy on the test set of ...

#### 3. Describe how certain the model is when predicting on each of the five new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 11th cell of the Ipython notebook.

For the first image, the model is relatively sure that this is a stop sign (probability of 0.6), and the image does contain a stop sign. The top five soft max probabilities were

| Probability         	|     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 98%        			| Wild Animals   									| 
|   .18   				| Right-of-way at the next intersection 										|
| .1076		| Traafic Signals											|
| .0005      			| Raodwork		 				|
| .00007			    | No entry      							|



### (Optional) Visualizing the Neural Network (See Step 4 of the Ipython notebook for more details)
#### 1. Discuss the visual output of your trained network's feature maps. What characteristics did the neural network use to make classifications?


