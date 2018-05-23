# **Traffic Sign Recognition** 

## Writeup

### You can use this file as a template for your writeup if you want to submit it as a markdown file, but feel free to use some other method and submit a pdf if you prefer.

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

You're reading it! and here is a link to my [project code](https://github.com/udacity/CarND-Traffic-Sign-Classifier-Project/blob/master/Traffic_Sign_Classifier.ipynb)

### Data Set Summary & Exploration

#### 1. Provide a basic summary of the data set. In the code, the analysis should be done using python, numpy and/or pandas methods rather than hardcoding results manually.

I used the pandas library to calculate summary statistics of the traffic
signs data set:

* The size of training set is 34799.
* The size of the validation set is 4410.
* The size of test set is 12630.
* The shape of a traffic sign image is (32*32*3).
* The number of unique classes/labels in the data set is 43.

#### 2. Include an exploratory visualization of the dataset.

Here is an exploratory visualization of the data set. It is a bar chart showing how many exmples per label.

![alt text][UDACITY_Project2/image_inRDME/imageLabelHistogram.png]

### Design and Test a Model Architecture

#### 1. Describe how you preprocessed the image data. What techniques were chosen and why did you choose these techniques? Consider including images showing the output of each preprocessing technique. Pre-processing refers to techniques such as converting to grayscale, normalization, etc. (OPTIONAL: As described in the "Stand Out Suggestions" part of the rubric, if you generated additional data for training, describe why you decided to generate additional data, how you generated the data, and provide example images of the additional data. Then describe the characteristics of the augmented training set like number of images in the set, number of images for each class, etc.)

As a first step, I decided to convert the images to grayscale because the color will not influence the result of the model. To handle with gray images will save the training time and memory.
Here is an example of a traffic sign image before and after grayscaling.

![alt text][./image_inRDME/colorandgraycompare.png]

As a last step, I normalized the image data because data normalization will make the data has slim distribution and make it easier to train.


#### 2. Describe what your final model architecture looks like including model type, layers, layer sizes, connectivity, etc.) Consider including a diagram and/or table describing the final model.

My final model consisted of the following layers:

| Layer         		|     Description	        					| 
|:---------------------:|:---------------------------------------------:| 
| Input         		| 32x32x3 RGB image   							| 
| Convolution 5x5     	| 1x1 stride, valid padding, outputs 28x28x6 	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 14x14x6 					|
| Convolution 5x5	    | 1x1 stride, valid padding, outputs 10x10x16	|
| RELU					|												|
| Max pooling	      	| 2x2 stride,  outputs 5x5x16 					|
| Convolution 1x1	    | 1x1 stride, valid padding, outputs 1x1x400	|
| RELU					|												|
| Fully connected		| outputs 120  									|
| Fully connected		| outputs 84  									|
| Fully connected		| outputs 43  									|
| Softmax				| etc.        									|
|						|												|
|						|												|
 


#### 3. Describe how you trained your model. The discussion can include the type of optimizer, the batch size, number of epochs and any hyperparameters such as learning rate.

To train the model, I used an AdamOptimizer to train my model.The batch size is 128. Number of epochs is  15. Learning rate is 0.001. the The probability of keeping applied in dropping out is 0.5.

#### 4. Describe the approach taken for finding a solution and getting the validation set accuracy to be at least 0.93. Include in the discussion the results on the training, validation and test sets and where in the code these were calculated. Your approach may have been an iterative process, in which case, outline the steps you took to get to the final solution and why you chose those steps. Perhaps your solution involved an already well known implementation or architecture. In this case, discuss why you think the architecture is suitable for the current problem.

My final model results were:
* training set accuracy of 0.998
* validation set accuracy of 0.958
* test set accuracy of 0.935

If an iterative approach was chosen:
* What was the first architecture that was tried and why was it chosen?
Lenet-5 architecture built in the lesson. Because it was easy to apply with a few changes.

* What were some problems with the initial architecture?
The problems with the first architecture were that it had low accuracy with training and validation data sets.

* How was the architecture adjusted and why was it adjusted? Typical adjustments could include choosing a different model architecture, adding or taking away layers (pooling, dropout, convolution, etc), using an activation function or changing the activation function. One common justification for adjusting an architecture would be due to overfitting or underfitting. A high accuracy on the training set but low accuracy on the validation set indicates over fitting; a low accuracy on both sets indicates under fitting.
Add a 1 by 1 convolution layer to improve the accuracy of both training and validation data sets. The adjust reason was that the 1 by 1 convolution layer could add more parameters without changing the architecture of the model. Also drop out was adding to the architecture. It could make the model to reduce over fitting.

* Which parameters were tuned? How were they adjusted and why?
The parameters of learning rate,epoch,batch size and drop out keep probability were tuned. The learning rate was first reduced according to my experience when accuracy was too low. Then I improved quantity batch size to feed more data in each training cycle. Finally I reduced the keeping probability of drop out to reduce the overfitting of the model.The epoch is enlarged to make the training suficiently.

* What are some of the important design choices and why were they chosen? For example, why might a convolution layer work well with this problem? How might a dropout layer help with creating a successful model?
For image classification, convolution layer works better because it can encode certain propeties into the architecture and reduce a lot of parameters to improve the training efficiency. Drop out could reduce overfitting of the model.

 

### Test a Model on New Images

#### 1. Choose five German traffic signs found on the web and provide them in the report. For each image, discuss what quality or qualities might be difficult to classify.

Here are six German traffic signs that I found on the web:

![alt text][./ImageForTest_my/1.png] ![alt text][./ImageForTest_my/2.png] ![alt text][./ImageForTest_my/3.png] 
![alt text][./ImageForTest_my/4.png] ![alt text][./ImageForTest_my/5.png] ![alt text][./ImageForTest_my/6.png]

The fourth image might be difficult to classify because it has more properties.

#### 2. Discuss the model's predictions on these new traffic signs and compare the results to predicting on the test set. At a minimum, discuss what the predictions were, the accuracy on these new predictions, and compare the accuracy to the accuracy on the test set (OPTIONAL: Discuss the results in more detail as described in the "Stand Out Suggestions" part of the rubric).

Here are the results of the prediction:

| Image			        |     Prediction	        					| 
|:---------------------:|:---------------------------------------------:| 
| 20km/h        		| 20km/h    									| 
| Priority road			| Priority road									|
| General caution		| General caution								|
| Road work	      		| Road work    					 				|
| 60km/h    			| 60km/h            							|
| Keep right  			| Keep right          							|


The model was able to correctly guess all of the signs, which gives an accuracy of 100%. This compares favorably to the accuracy on the test set of 93.8%. Although the accuracy on new images is pretty higher than test set result, it dose not mean the model is always correct. As the number of new images increase, the accuracy will reduce.

#### 3. Describe how certain the model is when predicting on each of the six new images by looking at the softmax probabilities for each prediction. Provide the top 5 softmax probabilities for each image along with the sign type of each probability. (OPTIONAL: as described in the "Stand Out Suggestions" part of the rubric, visualizations can also be provided such as bar charts)

The code for making predictions on my final model is located in the 28th cell of the Ipython notebook.



| Probability         	|    Prediction	             					| 
|:---------------------:|:---------------------------------------------:| 
| .998         			| 20km/h     									| 
| 1.     				| Priority road									|
| 1.					| General caution   							|
| .998	      			| Road work 					 				|
| .993				    | 60km/h             							|
| 1.				    | Keep right        							|
 





