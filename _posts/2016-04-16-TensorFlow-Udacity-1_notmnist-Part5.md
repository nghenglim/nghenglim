---
layout: post
title: TensorFlow Udacity 1_notmnist - Part 5
tags: [Machine-Learning,TensorFlow-Udacity]
---

![tensorflow-udacity]({{ site.baseurl }}/images/2016031900.png "tensorflow-udacity")

### Summary of 1_notmnist
Basically 1_notmnist is to learn how to display data in Jupyter Notebook. Besides, it also let us know on sklearn - a python machine library - so that we can then compare with TensorFlow. This is the exact [ipynb file at Tensorflow Github Repo](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/examples/udacity/1_notmnist.ipynb).

### Notice
This is as a form of sharing and discuss on better way to solve 1_notmnist problem. Do not copy and paste directly as it does not help on improving yourself + the answer is not optimized.

The entire series of TensorFlow Udacity can be found at [here](http://nghenglim.github.io/tags/#TensorFlow-Udacity-ref)


### Solving Problem 5
~~~python
def reshape(a):
    return a.reshape(a.shape[0],a.shape[1]*a.shape[2])
t = pickle.load(open("notMNIST.pickle", "r"))
unique_td = unique_rows(reshape(t['train_dataset']))
duplicate_rows = len(t['train_dataset']) - len(unique_td)
print(duplicate_rows)
~~~
![png]({{ site.baseurl }}/images/2016041600.png)

### Comment
Still got 2 optional question that I have not yet answered. Will get back to that in the future.
