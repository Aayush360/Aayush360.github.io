
## Image Segmentation.

assigning certain pixel color for one object and different pixel color for different object so that objects can be ditinguished in the image
is called image segmentation. (COLOR-CODING EACH PIXEL IN AN IMAGE)


## Validation and Test set:

Training the model using training set and evaluating on the same training set is like cheating or memorizing. 
i.e if we build a model to perform an addition, and for training we used just 3 numbers 1 ,2 ,5. The model could perform calculation on any combination of these
numbers like: 1+5=6. But, if we gave a new number like: 7 and perform addition: 1+7, it might give random results. Thus, we say that our model is overfitting.
In this case, we try to generalize our training set using more data.

Validation set are important to figure out the best model i.e selecting the right parameters for the model, so that the performance of our final model is as expected.
Validation set are sometimes called - hold-out set or development set.

If we have large dataset, set aside small fraction (generally depends on the size of overall dataset) for validation. This way, our model will not set these dataset
during training, thus will not get a chance to memorize. 

During cross-validation, we try to find the best model out of several models, and this is done by choosing right set of hyperparameters.
Hyperparameters can be thought as parameters about parameters.

Think of Parameters as weights and biases for the model, which is cruical for better model performance. The quality of parameters the model learns at the end of training
is determined by hyperparameters. Higher level choices that govern the meaning of weight parameter.

Some choices for hyperparameter could be: Learning rates, number of layers, number of hidden units, number of epochs, choice of activation function, data augmentation
strategies etc.

We can see how the model generalizes to new data using using validation set.

But we have one problem, just as the automatic training process is in danger of overfitting the training data, we are in danger of overfitting the validation data
through human trail and error and exploration. 


This lets us to introduce even more reserved data: **test set**.
As we prevented our model to see the validation set during training, we hide these test set from ourself during cross-validation.
This give us better insight of how our model performs in the real world, if the distribution of the data in test set is similar to that from the real world.

*The test and validation sets should have enough data to ensure that you get a good estimate of your accuracy*.

**Note: A key property of validation and test sets is that they must be representative of the new data you will see in the future**.


For timeseries data (the data that keep on updating as the funciton of time), it is not a good practice to select training and validation sets randomly.
The model will output gibberish result that won't give any insight. The better way to choose validation set is to select *continuous section* with the latest dates, 
and past *continous section* as the training data.

