## Jumping into Image Classification 

**Regular Expression**




**Presizing**
Data Augmentation strategy which when implemented: minimize data destrution while maintaining good performance. 

--------------------------------------------------------------------------------------------------------------------------------------------------------------------
**How CrossEntropy Loss in Pytorch works**

First Initialize the activation:
Here we have 6 images and we have to classify the image into one of the two categories:

**acts = torch.randn((6,2)) * 2**

**OUTPUT**

tensor([[-0.9916, -2.2545],
        [ 0.1560, -1.9368],
        [-0.6164,  1.1047],
        [-2.0798, -2.1778],
        [ 1.6429, -3.7728],
        [-1.2445, -2.9512]])

To take the softmax activation, it is equivalent to taking the difference of two activation for the same image and finally taking the sigmoid.
(See the derivation if not clear)

**(acts[:,0]-acts[:,1]).sigmoid()**

**OUTPUT**

tensor([0.7795, 0.8902, 0.1517, 0.5245, 0.9956, 0.8464])

Interpretation:
This means, for the first image our neural network is 0.7795(77.95%) sure it belongs to first category and (1-0.7795 = 0.2205), 22.05% sure it belongs to second category.

We can do the same calculation directly using the softmax function available in pytorch instead of deriving from a sigmoid.

**sm_acts = torch.softmax(acts, dim=1)**

**OUTPUT**

tensor([[0.7795, 0.2205],
        [0.8902, 0.1098],
        [0.1517, 0.8483],
        [0.5245, 0.4755],
        [0.9956, 0.0044],
        [0.8464, 0.1536]])
        

Let us assume our target variable is: 

targ = tensor([0,1,0,1,1,0])

This means, first image belongs to category 0, second image belongs to category 1, third image belongs to category 0 and so on....

To calculate loss from our prediction (sm_acts) and target value (targ), let's look at the prediction for the first image.
The actual or target value for the first image is 0, our model predicted the probability of this image to be 0.7795 for first category.
We know that the predicted value must be 0 to have zero loss, but our predicted value is much bigger than 0 i.e, 0.7795. So our loss is 0.7795.
This is the deviation from the target value.

Similarly, for our second image,the target value is 1, but our model predicted it to be 0.8902. So the deviation from the target value (loss) is: 1 - 0.8902 = 0.1098

We can calcuate it directly using a function call:

**F.nll_loss(sm_acts, targ, reduction='none')**

**OUTPUT**

tensor([-0.7795, -0.1098, -0.1517, -0.4755, -0.0044, -0.8464])

This is the same loss we calculate above but with a negative sign before the value.


To calculate the cross entropy loss in pytorch we use:

**nn.CrossEntropyLoss(reduction='none')(acts,targ)**

**OUTPUT**

tensor([0.2491, 2.2091, 1.8857, 0.7434, 5.4201, 0.1667])

TO derive the cross entropy loss, we take the **-ln(loss)** where ln is the natural log (with base e).

For the first image, our loss was 0.7795, so our cross entropy loss becomes: -ln(0.7795) = 0.2491.

For the second image, our loss was 0.1098, so our cross entropy loss becomes -ln(0.1098) =2.2091, which is the second value from our output tensor. 

Finally, to calculate the mean(average) of entire loss, we simply call **F.cross_entropy()** without passing reduction='none' parameter. 

**F.cross_entropy(acts,targ)**

**OUTPUT**

tensor(1.7790)



