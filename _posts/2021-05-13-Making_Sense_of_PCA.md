## Making Sense of Principal Component Analysis


I am writing this blog to assure myself I have gained necessary insight about the popular feature extraction and dimensionality reduction algorithm- Principal 
Component Analysis. I hope to share this concept in the simpliest way possible, though there is a lot of math involved behind the actual problem.

If we capture the real world data and try to make sense of it, we probably cannot do it just by looking at the numbers. Thus to make our task simple we go for
visualizing the data. But before that we should ask ourself a question- have we captured necessary variables about the data (i.e. the features that best explains 
the data)? If not, then that will be reflected as error or unexplained portion.

So hoping that we have captured few important variables that explains the data, we go for plotting it in carzy number of dimension we cannot even make sense of.
Also, too many features will give rise to problems like curse of dimensionality. Wouldn't it be great if we could just extract few most important features from the
pool of features and discard rest of them. Of course we can do that. This is where PCA comes handy.


PCA is a method of dimensionality reduction/ feature extraction that transforms the data from a d-dimensional space into a new coordinate system of dimension p, 
where p<=d. **In worst case scenario d = p** 

Say we have collected data that has 100 features for a house price prediciton problem. Features could be number of bedrooms, number of bathrooms, location, area,
and so forth counting all the way upto 100 features. But are all the features equally important? maybe not. Because, it might turn out that some feautres may account
for very little in explaining the dependent variable (house price in this case), or it might even explain nothing though there could be some correlation.
**As there is a popular saying Correlatin does not imply Causation.**

So we decided to choose say, only 3 features that best explains the data. But how to precisely choose features without loosing much of the informaiton from the original
data. We do it plotting the data first and choosing the direction (vector) that captures the first few maximum variation in the data.

So what are Principal Components in PCA? 
Well, the number of principal components we have is p which is the number of dimension we have after reducing the original dimension. The first principal component
is that direction that captures the maximum variation in the data. Similarly, second principal compoent explains the second maximum variation in the data and so forth.
The goal while reducing the dimension is to preserve as much of variance in the original data as possible in the new coordinate system.
The new variables that form a new coordinate system are called Principal Components.

Principal components are orthogonal linear transformation of the original variable. The principal component form a basis for the data. Susbets of p principal components
are chosen out of d (where d is the original dimension or number of feature we had). In order to approximate the space spanned by the original data points we can 
choose p based on what percentage of the variance of the original data we would like to maintain. 


I know ---- there is a lot of Linear Algebra jargons but let me explain it in layman terms relating to house price prediction examples.
Say there are 100 features in the original data like area, no of bedrooms, no of bathrooms, locality, and so forth out which: area alone can explain the price
of the house 50% accurately, no of bedrooms can account for 10%, no of bathroom can explain 10% and locality can explain 10% accurately. So, if we have only these
4 features out of 100 features we can explain/ predict house price (50+10+10+10)% = 80% accurately. So we maintain 80% of the variance in the original data just using
these 4 features. Let us assume the rest of 96 features explains only mimimum percentage of the total variance. Thus if we only keep these 4 features in our data
we are good to go, it will be computationally efficient and easy to get insight from them. Also saves us from the problem of Curse of Dimensionaltity.

We have done a great job here by changing the complex space of original data into simple 4 dimensional space without loosing much of the information. This is what
PCA does at high level overview......

But for mathematical insight, I will be covering it in my next blog post. 
*Till then, stay safe !!*


