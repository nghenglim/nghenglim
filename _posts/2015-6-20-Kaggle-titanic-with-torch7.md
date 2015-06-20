---
layout: post
title: Kaggle titanic challenge with torch7
---

![Kaggle Titanic Challenge]({{ site.baseurl }}/images/2015062000.png "Kaggle Titanic Challenge")

[Kaggle titanic challenge](https://www.kaggle.com/c/titanic) is a famous knowledge competition which many new Kaggler will try their
first Kaggle competition. Since there are currently no tutorial to solve this challenge with artificial neural network, I decided to use
torch7 to compete in this competition. FYI, [click here to get the data](https://www.kaggle.com/c/titanic/data). 

### Why Torch7

Deep learning is state of the art machine learning algorithm in learning image, video, sound and natural language.
[Torch7](http://torch.ch/) is one of the famous deep learning framework, which is already used within Facebook, Google, Twitter, NYU, 
IDIAP, Purdue and several other companies and research labs.

### Model

![Learning Model]({{ site.baseurl }}/images/2015062001.png "Learning Model")

### Validation

Validation is using back the training dataset since the dataset will be too small if I separate it. As I am using tanh as transfer function
, for those model output bigger than 0, I classified it as survived. Using model after training for 20000 epoch, the result are:

- False Positive : 31
- True Positive : 276
- False Negative : 66
- True Negative : 518

### Submission Result

The score is the percentage of passengers we correctly predict. The submission result using model on epoch 20000 is 0.74641. From the 
result, we know that our model is slightly overfitted because training set accuracy is 89.113% while test set is 74.646%.

### Some Thought

I have showed that torch7 works in Kaggle titanic challenge too. With this method, I can easily get the probability that a passenger is 
survived based on the input, and this Bayesian behavior is really important in real world use case.

### Some Picture
![Torch7]({{ site.baseurl }}/images/2015062003.png "Torch7")