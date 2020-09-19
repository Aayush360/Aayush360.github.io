#Reading paper: Cyclical Learning rates for training Neural Network

**From further research portion of Deep Learning for Coders Book(Chapter 5: Image Classification)**

For training a deep neural network, we have to perform lot of hyperparameter tuning. Finding the optimal value for hyperparameters like: learning rate, mini batch
size, no of hidden units for each layers, number of layers, beta parameter in adam optimizer etc. for a deep neural network is crucial for better performance of our 
model so that our model generalizes in the real world. 

Among these hyperparameters, learning rate is most important to be tuned. The author in this paper describes a method called cyclical learning rate, where learning 
rate varies between reasonable boundary values. Instead of fixed value, this shows improvements in classification accuracy and in fewer iterations. According to them,
CLR method practically eliminates the need to tune the learning rate and achieve near optimal classification accuracy.

Unlike apdative learning rate, this method requires no additional computation.

The main idean is letting the learning rate vary within a range of values rather than adopting a stepwise fixed or exponentially decreasing value. That is, one sets
minimum and maximum boundaries and the learning rate cyclically vary between these bounds. 

Paper illustrates the traingular window functional form as it is simple function to incorporate the idea. This is termed as traingular learning rate policy.

**Implementation of the code for new learning rate policy:**

*local cycle = math.floor( 1 + epochCounter / (2 * stepsize))*

*local x = math.abs( epochCounter / stepsize - 2 * cycle + 1)*

*local lr = opt.LR + (maxLR -opt.LR) * math.max(0, (1-x))*

opt.LR is specified lower learning rate
epochCounter is the number of epochs of trainig caculcated as (no. of training example / batch_size)
lr is computer learning rate

![Triangular Learning rate policy](images/CLR.png)


 The policy is called traingular because of the two parameter defined : stepsize (half the period or cycle length) and max_lr is maximul learning rate boundary.
 
 This code varies the learning rate linearly between minimum (*base_lr*) and maximum(*max_lr*).




**For computing epochCounter (length of cycle) and stepsize:**

epoch = total training instances/batch_size

stepsize = (2 to 10)* epochs 

This method simplifies the decision of when to drop the learning rate and when to stop the current training run (when the *lr* is at minimum and the accuracy peaks.)
Replacing each step of constant learning rate with at least 3 cycles trains the n/w weights most of the way and running for 4 or more cycles will achieve even better
performance.

**Estimating reasonable minimum and maximum boundary vaues**

Using LR Range test- it says, run your model for several epochs while letting the learning rate increase linearly between low and high LR values.
This test is valueable when you are facing new architecture or datsets. 

Here set you base_lr and max_lr. set step_size and max_iter to same number of iterations and run. plot accuracy vs learning rate.
Note the learning rate value when the accuracy starts to increase and when the accuracy slows, becomes ragged, or starts to fall. These two learning rate are good 
choices for the bounds.

This LR range test provides good LR value and a good range. Compare runs with fixed LR vs CLR with this range. Whichever wins can be used with confidence for rest of 
one's experiment with the new architecture or datset.
