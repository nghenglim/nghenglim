---
layout: post
title: Paper reading - Weight Uncertainty in Neural Networks.
---

![nn vs Bayes by Backprop]({{ site.baseurl }}/images/2015052300.png "nn vs Bayes by Backprop")

This [paper](http://arxiv.org/pdf/1505.05424.pdf) is published by Google DeepMind. 

### Background

Backpropagation, is a well known learning algorithm in neural network. In the algorithm, 
the weight calculated is based on the out put of the result. To prevent overfitting and 
introduce more uncertainty, its often comes with L1 and L2 regularization.

Weights with greater uncertainty introduce more variability into the decisions made by the
network, leading naturally to exploration

### Reading

This article introduced a new regularization method called Bayes by Backprop.

Instead of a fixed value, they view neural network as a probabilistic model.

![No-Drop vs DropOut vs DropConnect]({{ site.baseurl }}/images/2015052400.png "No-Drop vs DropOut vs DropConnect")

In Dropout or DropConnect, randomly selected subset of activations are set to zero within each layer. However in
Bayes by Backprop, the activation is set based on its probability. When the dataset is big enough, 
its similar to the usual backpropagation algorithm, with more regularization.

### Result

1. When classifying MNIST digits, performance from Bayes by Backprop(1.34%) is comparable to that of
Dropout(~=1.3%), although each iteration of Bayes by Backprop is more expensive than Dropout –
around two times slower).
2. In MNIST digits, Dropconnect(1.2% test error) perform better than Bayes by Backprop.

### Personal Thought

This paper comparison based on MNIST test error is not accurate enough, we should compare its false
positive result with human eye classification - as some of MNIST labelling is arguable.

Bayes by Backprop might achieve higher performance in specific situation. 