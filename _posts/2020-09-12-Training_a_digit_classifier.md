# What I learned from Training a Digit Classifier.

**Creating a baseline first**: 
Instead of make a complex model in the first go, start with simple and easy to implement model.
Here we started with a simple concept of measuring the difference in pixel value between the compared image: one being the ideal image we have calculated using 
the mean of entire image for each pixel position, and the other - a sample image we like to classify (either as 3 or 7 in this case).

We can also search for other people's code which resemble our project plan(problem/objectie) and download adn run it on our dataset. 

**How a tensor differs from Numpy array**.

**Concept of Broadcasting in Pytorch (also, applicable to Numpy)**:
Expands the tensor with smaller rank to have the same size as the one with higher rank.
A simple example would be adding a real number to a list: [1,2,3] + 3 = [4,5,6]. Here 3 is being broadcasted to entire list of [1,2,3] and added to individual element.
We dont need to tell the rank of 3 explicitly. 

* memory efficient 
* very fast than pure python, where we should have implemented using loops (very inefficient). Insead, here the whole calculation is occurs in C or CUDA. 
