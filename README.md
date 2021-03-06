# **Behavioral Cloning** 


**Behavioral Cloning Project**

The goals / steps of this project are the following:
* Use the simulator to collect data of good driving behavior
* Build, a convolution neural network in Keras that predicts steering angles from images
* Train and validate the model with a training and validation set
* Test that the model successfully drives around track one without leaving the road
* Summarize the results with a written report


[//]: # (Image References)

[image1]: ./examples/model.png "Model Visualization"
[image2]: ./examples/image2.jpg
[image3]: ./examples/image3.jpg "Recovery Image"
[image4]: ./examples/image4.jpg "Recovery Image"
[image5]: ./examples/image5.jpg "Recovery Image"
[image6]: ./examples/image2.jpg "Normal Image"
[image7]: ./examples/image7.jpg "Flipped Image"

## Rubric Points
### Here I will consider the [rubric points](https://review.udacity.com/#!/rubrics/432/view) individually and describe how I addressed each point in my implementation.  

---
### Files Submitted & Code Quality

#### 1. Submission includes all required files and can be used to run the simulator in autonomous mode

My project includes the following files:
* model.ipynb containing the script to create and train the model
* drive.py for driving the car in autonomous mode
* model.h5 containing a trained convolution neural network 
* README.md summarizing the results

#### 2. Submission includes functional code
Using the Udacity provided simulator and my drive.py file, the car can be driven autonomously around the track by executing 
```sh
python drive.py model.h5
```

#### 3. Submission code is usable and readable

The model.ipynb file contains the code for training and saving the convolution neural network. The file shows the pipeline I used for training and validating the model, and it contains comments to explain how the code works.

### Model Architecture and Training Strategy

#### 1. An appropriate model architecture has been employed

My model consists of a convolution neural network with 5x5 filter sizes and depths between 16 and 64 (model.ipynb) 

The model includes RELU layers and linear layers to introduce nonlinearity (model.ipynb), and the data is normalized in the model using a Keras lambda layer (model.ipynb). 

#### 2. Attempts to reduce overfitting in the model

The model contains dropout layers in order to reduce overfitting (model.ipynb). 

The model was trained and validated on different data sets to ensure that the model was not overfitting (model.ipynb). The model was tested by running it through the simulator and ensuring that the vehicle could stay on the track.

#### 3. Model parameter tuning

The model used an adam optimizer, so the learning rate was not tuned manually (model.ipynb).

#### 4. Appropriate training data

Training data was chosen to keep the vehicle driving on the road. I used a combination of center lane driving, recovering from the left and right sides of the road and fliping the center lane driving images.

For details about how I created the training data, see the next section. 

### Model Architecture and Training Strategy

#### 1. Solution Design Approach

The overall strategy for deriving a model architecture was to train the model to get a low error loss in the validation data and test the model behavior in the simulation to drive properly.

My first step was to use a convolution neural network model similar to the LeNet I thought this model might be appropriate because it's simple to get start and easy to expand.

In order to gauge how well the model was working, I split my image and steering angle data into a training and validation set. I found that my first model had a low mean squared error on the training set but a high mean squared error on the validation set. This implied that the model was overfitting. 

To combat the overfitting, I modified the model by adding dropout layers so that it can avoid overfitting.

Then I trained the data and the error on the validation set is similar to the training set .

The final step was to run the simulator to see how well the car was driving around track one. There were a few spots where the vehicle fell off the track such as the turning place. To improve the driving behavior in these cases, I expand the data set by adding left image and right image and flipping the center image.

At the end of the process, the vehicle is able to drive autonomously around the track without leaving the road.

#### 2. Final Model Architecture

The final model architecture (model.ipynb)  is showed by model.summary().
Here is a visualization of the architecture 

![alt text][image1]

#### 3. Creation of the Training Set & Training Process

To capture good driving behavior, I first recorded two laps on track one using center lane driving. Here is an example image of center lane driving:

![alt text][image2]

I then recorded the vehicle recovering from the left side and right sides of the road back to center so that the vehicle would learn to recover. These images show what a recovery looks like starting from right to middle :

![alt text][image3]
![alt text][image4]
![alt text][image5]

Then I repeated this process on track two in order to get more data points.

To augment the data set, I also flipped images and angles thinking that this would expand the scene and improve the accuracy. For example, here is an image that has then been flipped:

![alt text][image6]
![alt text][image7]



After the collection process, I had 8036 number of data points. I then preprocessed this data as followers:
- convert the BGR image to RGB image
- apply correction parameter to the angle of left image and right image
- flip the center image
- normalize the image
- crop the top and bottom lines in order to reduce unrelated information

I finally randomly shuffled the data set and put 20% of the data into a validation set. 

I used this training data for training the model. The validation set helped determine if the model was over or under fitting. The ideal number of epochs was 4 (model.ipynb). I used an adam optimizer so that manually training the learning rate wasn't necessary.
