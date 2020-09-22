# Image Regression

When I first heard about the term image regression, I thought it might be something quite complex. But the general idea is simple. 
This is one class of problem which considers image to be an input to the model (i.e, the independent variable), and the output(target) from the model (dependent variable)
is one or more floats (i.e some real values of some dimension).

Here we have considered dataset from : Biwi Kinect Head Pose Dataset, which contains different pose of same person organized into a folder(directory) and has 
collection of such folders. Simply, each folder contains multiple different pose of a same person, and the entire dataset is the collection of such folders.

The choice of model we have used is: key point model where the dependent variable is simply a keypoint (feature) for an image. A *keypoint* refers to a specific location
represented in an image - in this case we have used images of people and we have looked for center of person's face in each image. 

Keypoints are important features for for CNN Model used for pose estimation, emotion classifier et

We have built a model that takes such images as an independent variable and the coordinates for the center of the face as the dependent variable. 
So, in this case our dependent variable is simply a vector with 2 values (x and y coordinates) for a single image.

And the output from the model is also a coordinate for each image which marks the center of the face. If our model is accurate, the point predicted as the center of the
face should be as close to the actual point present in the image label.
For the loss function, we have chosen mean squared error (default), which calculates how far is the distance of the predicted point from the actual point. The closer the
distance, the better is the model. 

Since unit of MSE is squared, for evaluation (as a choice of metrics) we use root mean squared error (rmse). This way, it is more readable and interpretable.




We can treat image regression as a variant of CNN problem but we should be able to understand how to prepare a datablock.
Here we made our datablock API using:

**get_image_files** function: that locates the images from the path object

**get_ctr** function : this is the function we created, which takes image as an input, finds the corresponding labels (having the same name but with _pose.txt extension) and
          finally calculates the center of face for that image returning coordinates in the form of tensor ([c1,c2])

It takes **PointBlock** as label block, to tell fast ai, the label contains coordinates, this way while doing data augmentation, it should do the same augmentation
to these coordinates as it does to the images.


When creating a learner, we used y_range=(-1,1). It is because coordinates in fastai and Pytorch are always rescaled between -1 and +1.
y_range is implemented as follows:

*def sigmoid_range(x, lo, hi):*

  *return torch.sigmoid(x) * (hi-lo) + lo*
  
**Interpretation of this function**

for any point we provide : say, x - it is first passed into a sigmoid function that squashes the output between 0 (if big negative value) and 1 (if big positive value)
this is then multiplied with (hi-ho) which gives (1-(-1)) = 2
finally everything is added to -1.

**Case 1: if x is big negative number**

* for demo, let's take x = -50
* passing it to simoid gives something close to 0,
* multiplying this to (hi-lo) =2, gives something close to 0 as well
* finally 0-1=-1 , which gives output closer to -1 (little greater than -1 but never smaller)


**Case 2: if x is big postive number**

* passing x=50 to sigmoid gives something close to 1,
* multiplying it to (hi-lo)=2 gives something close to 2 (little less)
** finally 2-1=1, which gives output that approaches 1 from the left side.


**Case 3: if x is zero**

* passing x=0 to sigmoid gives 0.5
* multiplying to (hi-lo)=2 gives, 0.5*2 = 1
** finally 1-1=0, gives output exacly equal to 0.



**This shows that the function *sigmoid_range()* forces the model to output activations in the range of (hi,lo), which we have taken to be (-1,1).**


Using flexible datablock API and making the use of transfer learning, we fine-tuned our pretrained model to perform image regression, although it was trained to do
image classification.


**Choice of Loss function for different task:

* nn.CrossEntropyLoss for single label classification
* nn.BCEWithLogitsLoss for multi-label classification
* nn.MSELoss for regression

                                               
                                               
                                               
                                               
                                               HAVE A GOOD DAY!!



