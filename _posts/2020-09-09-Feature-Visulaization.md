
## What our Image-Recognizer Learns? 

*Learnings from [paper]((https://arxiv.org/pdf/1311.2901.pdf)) by Zeiler and Fergus. They extracted these activations while using AlexNet (consisted of 5 layers) trained on ImageNet dataset.*


We know that a neural network has multiple layers depending upon its complexity. To carry out complex learning from lot of datas, many layers are inserted between
the input and the output layer. They are refrred to has hidden layers.
A neural network with many layers (>=3) is considered a deep neural network.

**Note**: Input layer is not considered as the layer. Rather, it is the feature (parameter) that our model takes for learning. 
If our Neural Network has 4 layers, it means: it has 3 hidden layers and 1 output layer.

The more the number of layers, the more complex features it can learn.
Generally, the initial hidden layer(layer-1) learns simple features like: edges, textures. Layer-2 takes these features and builds upon it to create even complex 
features like shapes and patterns. With increase in number of hidden layers, the features also tends to be more complex, gradually building to faces and objects
we are trying to identify.

*Prior to deep learning era, these features were handcrafted.*
