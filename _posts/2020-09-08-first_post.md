# HELLO UNIVERSE!

THIS IS MY FIRST PAGE.

## Book: Deep Learning for Coders with fastai and PyTorch
Chapter1: Your Deep Learning Journey: 

### What is Machine Learning ? 

Training a computer/machine to perform an action and give sensible result, without writing every single step as in regular computer programming. 
Generally, learning happens from the data given to the algorithm.
Heart of machine learning involves algorithm, that takes the data - either labeled or unlabeled and makes the decision or prediction. 

*Supervised, Unsupervised and Reinforcement Learning are its type.*


**Weights**: They are variables that keep on changing(updating) as the algorithm learns so as to give the best output possible (minimize the loss/ maximize the accuracy)

**Model**: Just a fancy term for a program or a main-box(heart) . It takes parameters like weights and biases as an input along with actual input (features), which ultimately determines the performance of the model. Model can also be thought as the *architecture. 

Classification model: outputs discrete values, 0 or 1 (for example) in case of binary classication model (also called classifier)

Regression model: outputs continuous values like :Rs. 1200 in case of price predicting model, or 12 degree in case of temperature predicting model.

**Trained Model **: Once the choice of weights and biases becomes suitable for the model to give desired result, it will become the part of the trained model.
The trained model can be thought of as a trained computer program. 

### What is a Neural Network?

A flexible function that solve any given problem just by varying the weights (parameters). And to find the right weights, we can generally use Stochastic Gradient Descent *(SGD)* optimizer. 
To evaluate how well our model does, we can use *accuracy*  (no. of correct prediction out of all question) OR *Loss* as the performance metrics (for now!).


The larger the image size, better is the result(accuracy) of the model but in expense of speed and memory consumption. It is because the model can learn fine details present in the high resolution image, which have more information embedded in the form of pixels.

**Validation sets** are datasets which is part of the training set and are held-out(not used in training the model) to evaluate the performance of the model and tune the parameters. This makes sure our model does a good job even in previouly unseen datasets. This will prevent overfitting of the model and give more generalized result. Overfitting is like memorizing from little data, but generalizing poorly on unseen data.

Better to look at the performance on training and validation set to evaluate if your model is overfitting before actually performing overfitting avoidance techniques (Regularization, Dropout etc). If you have enough data for training, the model might not overfit. 

Larger model (with many layers) are more likely to overfit because of their complexity. It can easily memorize the data given to it. But if we have enough data, this won't probably happen. 

**Metric**: A function that measures how well our model performs on the validation set. error_rate and accuracy (1-error_rate) are some examples. Metric is used by human to interpret the model's performance easily. 
Unlike loss, which is used by the model to update the weights. The main purpose of training is to minimize the loss function being defined. 

**Pretrained model**: Has weight it has learned from another dataset. This model can be modified slightly depending on the dataset size you have, as it can generalize to things like edges, colors, gradient and other low level features which are almost similar in differet images. 
The last part of the model which makes prediction (depending on the number of classes you need) is called *head*. 
Using the pretrained model for task different from what it was originally trained on is called **transfer learning**.

**Fine-tuning** is done to pre-trained model during transfer learning to continue to learn new parametres from what it has already learnt (not from the beginning). 
New parameters added to the pretrained models(usually at the head of the model) are updated faster than the earlier parameters we had.

An **epoch** is a complete pass through the entire dataset.


