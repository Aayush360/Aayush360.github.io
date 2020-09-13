# What I learned from Training a Digit Classifier.

**Creating a baseline first**: 
Instead of make a complex model in the first go, start with a simple and easy to implement model.
Here we started with a simple concept of measuring the difference in pixel value between the image being compared: one being the ideal image we have calculated using 
the mean of entire image for each pixel position, and the other - a sample image we like to classify (either as 3 or 7 in this case).

We can also search for other people's code which resemble our project plan(problem/objective); download and run it on our dataset. 

**How a tensor differs from Numpy array**.

**Concept of Broadcasting in Pytorch (also, applicable to Numpy)**:
Expands the tensor with smaller rank to have the same size as the one with higher rank.
A simple example would be adding a real number to a list: [1,2,3] + 3 = [4,5,6]. Here 3 is being broadcasted to entire list of [1,2,3] and added to individual element.
We dont need to tell the rank of 3 explicitly. 

* memory efficient 
* very fast than pure python, where we should have implemented using loops (very inefficient). Insead, here the whole calculation is occurs in C or CUDA. 

**Stochastic Gradient Descent**

To make learning automated we use SGD. Basic Idea is to allow model to assign higher weight to the corresponding pixel which is likey to get activated for a given digit. 

While taking a step towards minimum, we can control the step size using a *learning rate*. 
Right value for learning rate is an important factor for convergence of loss. If we take very small value for the learning rate, it will take long time to converge
or to find the global minima, and if we take very large value, it will bounce randomly never taking a right path towards the minima. 


**The reason we cannot use accuracy as our loss metric**

Slope is defined as rise over run; or (height/width); (change in functional value/change in input value) and different version of the same story.

In short, what will be the change in functional value when we made a very small tweak to our input value. 
In case of neural network, the entire network can be thought as a function and the output from this network is the prediciton.
Input can be thought as the weights. So, to calculate gradient, we make a small tweak to the weight and see how it will affect the final prediction from the model.

While making a system to predict if the digit is 3 or 7, the accuracy only changes when the model misclassifies (i.e. 3 for 7 or 7 for 3).
Thus small change in w does not bring change in the accuracy (there is no change in prediction). This causes our gradient to be 0, which will leave our model to learn nothing.


Learning happens by updating the weight: **w_new = w_old - learning_rate * change_in_output_wrt_change_in_weights**
when gradient is 0, it means the term : change_in_output_wrt_change_in_weights is 0. In this case the above update rule becomes: **w_new = w_old - learning_rate * 0** 
This gives: w_new = w_old; thus the weight new changes and no learning happens. 

**Why loss must be a sensible function**

Loss is a function our model implements for learning and improving on it's own. Unlike, accuracy which is used often by human to get insight of the model performance. It is important that we learn to focus on these metrics, rather than the loss, when judging the performance of the model.

While choosing a loss function we should choose one that is reasonably smooth (less bumps and plateaus) so that it can be optimized using the gradient.
The loss function is calculated for each item in our datset and at the end of the epochs the loss values are all averaged and the overall mean is reported for the epoch.

**Sigmoid Activation Funtion**

This is the function that takes any input value, positive or negative and smooshes it into an output value bwtween 0 and 1.
For larger positive value, it gives output very close to 1; and for larger negative values, it gives output very close to 0.
If we give 0 as an input, it outputs 0.5 : 1/(1+exp(-0))=0.5.
*Note: Although it is non-linear function, if we consider its small middle part close to 0, it resembles a linear function.*
