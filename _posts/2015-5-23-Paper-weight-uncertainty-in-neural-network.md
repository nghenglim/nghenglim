---
layout: post
title: Paper reading - Weight Uncertainty in Neural Networks.
---

![an image alt text]({{ site.baseurl }}/images/2015052300.png "nn vs Bayes by Backprop")

This [paper](http://arxiv.org/pdf/1505.05424.pdf) is published by Google DeepMind. 

### Background

Backpropagation, is a well known learning algorithm in neural network. In the algorithm, 
the weight calculated is based on the out put of the result. To prevent overfitting and 
introduce more uncertainty, its often comes with L1 and L2 regularization.

Weights with greater uncertainty introduce more variability into the decisions made by the
network, leading naturally to exploration

### Reading

This article introduced a new regularization method called Bayes by Backprop.

(Still spending time looking the proof, will continue this post after finished)