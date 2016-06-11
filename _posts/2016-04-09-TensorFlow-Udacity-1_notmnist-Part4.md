---
layout: post
title: TensorFlow Udacity 1_notmnist - Part 4
tags: [Machine-Learning,TensorFlow-Udacity]
---

![tensorflow-udacity]({{ site.baseurl }}/images/2016031900.png "tensorflow-udacity")

### Summary of 1_notmnist
Basically 1_notmnist is to learn how to display data in Jupyter Notebook. Besides, it also let us know on sklearn - a python machine library - so that we can then compare with TensorFlow. This is the exact [ipynb file at Tensorflow Github Repo](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/examples/udacity/1_notmnist.ipynb).

### Notice
This is as a form of sharing and discuss on better way to solve 1_notmnist problem. Do not copy and paste directly as it does not help on improving yourself + the answer is not optimized.

The entire series of TensorFlow Udacity can be found at [here](http://nghenglim.github.io/tags/#TensorFlow-Udacity-ref)


### Solving Problem 4
~~~python
print(np.unique(train_labels))
print(np.unique(test_labels))
print(np.bincount(train_labels))
print(np.bincount(test_labels))
~~~
![png]({{ site.baseurl }}/images/2016040900.png)

### Comment
Since after shuffling, the image for each count for each train_labels and test_labels is the same, therefore we can say that the data is still good after shuffling!
