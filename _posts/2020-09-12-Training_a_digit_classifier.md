# What I learned from Training a Digit Classifier.

**Creating a baseline first**: 
Instead of make a complex model in the first go, start with a simple and easy to implement model.
Here we started with a simple concept of measuring the difference in pixel value between the image being compared: one being the ideal image we have calculated using 
the mean of entire image for each pixel position, and the other - a sample image we like to classify (either as 3 or 7 in this case).

We can also search for other people's code which resemble our project plan(problem/objective); download and run it on our dataset. 

**How a tensor differs from Numpy array**.

Numpy does not support using the GPU or calculating gradients whereas PyTorch tensor supports both.

Numpy array a is multidimensional table of data, with all items of the same type.

Unlike Numpy array, tensor cannot have jagged structure and also has a restriction that it cannot use any old type- it has to use a single basic numeric type for all components. But like Numpy array, it is also a multidimensional tabel of data, with all items being the same type.


Rank of a tensor is the number of dimension it has whereas, shape of a tensor is number of elements(pixels) in each dimension.
For example, in Pytorch if shape of a tensor is [200,30,30], it means we have 200 images each having height and width of 30 pixels. 

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
This is also called an optimization step.
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

**MiniBatch Tradeoff**

If you use minibatch size that is too small, you would get unstable gradient (utilize very little information from small set of examples or mini-batches) and the loss function might never converge -wander near optimum value.
If you use minibatch size that is too large, you will have to wait too long to get the insight of how well your model is doing. But this is stable.
We have to choose mini-batch size that is neither too small or too big. 
Also, in each epoch we randomly shuffle the training data to make a mini-batch. 


**I found a intuitive definition of a neural network in terms of nonlinearity**

If we add some non-linearity(something that does not give a linear graph on plotting) between two linear function, this gives us a neural network.

**Explanation:**

Consider a node that take as an input W,X,b and computes W * X + b ; this is then passed to a non-linear function like reLU or tanH or Sigmoid or you name it,
if reLU: it computes: max(0, W * X +b). This is called the activation 'A' from that node. This activation is passed to another node in the next layer which first calculates the linear function: W * A + b and passes this output to non-linear function and so on. 

Rectified linear unit abbreviated as ReLU, is a non-linear function that changes every negavtive number to 0 and leaves the positive number unchanged.

**Adding more linear layers is predictable, it just another linear function**

Composition of two linear function is itself a linear function. If we're not using any non-lineariy between layers, we are not computing more interesting functions even if we go deeper into the network. 


Series of any number of linear layers in a row can be replaced with a single linear layer with a different set of parameters. 
But if we put non-linear funtion between them it is no longer true. 
Sometimes, you can use linear activation in the output layer, else it not used frequently. 

Finally we build a neural network with 784 input parameters (28* 28), first hidden layer with 30 hidden units(nodes) whose output is passed to a ReLU non-linearity, 
and an output layer with a single node(unit). We used Stochastic Gradient Descent as our optimizer and trained for 40 epochs with learning rate 0.1. This yielded 
batch_accuracy of 98.47. We used mnist_loss as our loss function which was minimized to the value of 0.0184. 

Batch accuracy: Number of correct prediction expressed in percentage.
mnist_loss: Calculates the average deviation from the actual value.

**Definition of mnist_loss fucntion**

def mnist_loss(predictions, targets):
  predictions = predictions.sigmoid()
  return torch.where(targets==1, 1-predictions, predictions).mean()
