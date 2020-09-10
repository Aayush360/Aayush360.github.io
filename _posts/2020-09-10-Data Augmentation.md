## Data Augmentation

As we know, due to model's complexity they might tend to overfit the training data - or memorize the patterns, so that they might not generalize well on new datas.
To prevent such overfitting we use Regularization Teachniques.

One of the obvious solution could be to use more data during training the model.
As we know that if our model is too big or complex with little data fed during training, it will perform nearly perfectly and overfit. So, giving the model more data
we can prevent overfitting.

As gathering data could be cumbersome, data augmentation process becomes life saviour approach. 
It can be thought as an inexpensive and fastest way to give your algorithm more data from whatever you have gathered by simple modifications on them.
This is the process of creating random variations of our input data such that they appear different but do not change the meaning of the data.

Eg, rotating a dog's image slightly is still a dog. 

It is better if you can get brand new data, but data augmentation can still makes the task simpler.

Some ways of Data Augmentation are:
* Horizontal flipping (mirroring)
* random crop
* shifting or translating
* rotating
* Shearing
* Perspective wraping
* contrast and brightness changes

Areas like Computer Vision need large amount of data. Thus Data Augmentation helps to generate or multiply images for the hungry models. 

**Color Shifting** is also an example of Data Augmentation, ie., changing the pixel intensity of various color channels. This makes your learning algorithm more
robust to changes in the colors of your images.

Applying these augmentations to batches of images using the GPU will save lot of time, rather than applying on a single image one at a time. 
