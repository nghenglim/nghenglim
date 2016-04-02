---
layout: post
title: TensorFlow Udacity 1_notmnist - Part 3
tags: [Machine-Learning,TensorFlow-Udacity]
---

![tensorflow-udacity]({{ site.baseurl }}/images/2016031900.png "tensorflow-udacity")

### Summary of 1_notmnist
Basically 1_notmnist is to learn how to display data in Jupyter Notebook. Besides, it also let us know on sklearn - a python machine library - so that we can then compare with TensorFlow. This is the exact [ipynb file at Tensorflow Github Repo](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/examples/udacity/1_notmnist.ipynb).

### Notice
This is as a form of sharing and discuss on better way to solve 1_notmnist problem. Do not copy and paste directly as it does not help on improving yourself + the answer is not optimized.

The entire series of TensorFlow Udacity can be found at [here](http://nghenglim.github.io/tags/#TensorFlow-Udacity-ref)


### Solving Problem 3
~~~python
len_dict = {}
for folder in folder_names:
    t = pickle.load(open(dir_name + "/" + folder + ".pickle", "r"))
    len_dict[folder] = len(t)
print(len_dict)
~~~
![png]({{ site.baseurl }}/images/2016040200.png)

### Comment
Since the image for each class is roughly around 52911, therefore we can say that the data is balanced. Though more appropiate way is to calculate the standard deviation :)
