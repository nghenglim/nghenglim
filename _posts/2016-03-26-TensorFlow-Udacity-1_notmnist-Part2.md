---
layout: post
title: TensorFlow Udacity 1_notmnist - Part 2
tags: [Machine-Learning,TensorFlow-Udacity]
---

![tensorflow-udacity]({{ site.baseurl }}/images/2016031900.png "tensorflow-udacity")

### Summary of 1_notmnist
Basically 1_notmnist is to learn how to display data in Jupyter Notebook. Besides, it also let us know on sklearn - a python machine library - so that we can then compare with TensorFlow. This is the exact [ipynb file at Tensorflow Github Repo](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/examples/udacity/1_notmnist.ipynb).

### Notice
This is as a form of sharing and discuss on better way to solve 1_notmnist problem. Do not copy and paste directly as it does not help on improving yourself + the answer is not optimized.

The entire series of TensorFlow Udacity can be found at [here](http://nghenglim.github.io/tags/#TensorFlow-Udacity-ref)


### Solving Problem 2
~~~python
# first load the pickle file, loading one for illustration purpose
t = pickle.load(open("notMNIST_large/A.pickle", "r"))
# need to use matplotlib inline if want to show at jupyter Notebook
%matplotlib inline
# plot one of image. the number 5 to be exactly
plt.imshow(t[4], interpolation='nearest')
# show the image
plt.show()
~~~
![png]({{ site.baseurl }}/images/2016032600.png)
