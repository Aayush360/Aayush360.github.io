## Building Emotion Classfier:

Trying out Bear Classifer with different dataset to make an Emotion Classifier:

Can I get images of people with different emotions - happy, sad, angry ? - YES! 

First of all I implemented it on Goolge Colab, and the performance was quite worse. Even after cleaning the data and running for 9 epochs, I got an error rate of
0.352273. I then tested it on couple of obvious images, and it worked !!
I then wanted to deploy the model, when i came across the command : **!jupyter serverextension enable voila --sys-prefix** I realized I had to used Jupyter Notebook,
not Google Colab.

When I moved my codes to jupyter Notebook, without changing any parameters,  I got an error while training. 
something like: **RuntimeError: DataLoader worker (pid 2063) is killed by signal: Unknown signal: 0.*Stii*

I tried to understand the error and got to know that It was due to out of memory problem.
To resolve it: I changed by batch_size to 16 instead of default=64. I also decreased image size to 128 instead of 224 being used originally.
But the error persisted. 


 Still working on it! Positive ...
