---
layout: post
title: TensorFlow Udacity 1_notmnist - Part 1
tags: [Machine-Learning,TensorFlow-Udacity]
---

![tensorflow-udacity]({{ site.baseurl }}/images/2016031900.png "tensorflow-udacity")

### Summary of 1_notmnist
Basically 1_notmnist is to learn how to display data in Jupyter Notebook. Besides, it also let us know on sklearn - a python machine library - so that we can then compare with TensorFlow. This is the exact [ipynb file at Tensorflow Github Repo](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/examples/udacity/1_notmnist.ipynb).

### Notice
This is as a form of sharing and discuss on better way to solve 1_notmnist problem. Do not copy and paste directly as it does not help on improving yourself + the answer is not optimized.

The entire series of TensorFlow Udacity can be found at [here](http://nghenglim.github.io/tags/#Tensorflow-Udacity-ref)

### Preparation
~~~bash
# start a docker container
docker run -p 8888:8888 -it b.gcr.io/tensorflow-udacity/assignments:latest
~~~

>### Problem 1
>Let's take a peek at some of the data to make sure it looks sensible. Each exemplar should be an image of a character A through J rendered in a different >font. Display a sample of the images that we just downloaded. Hint: you can use the package IPython.display.

### Solving Problem 1
~~~python
import os, random
dir_name = "notMNIST_large"
folder_names = ["A", "B", "C", "D", "E", "F", "G", "H", "I", "J"]
for folder in folder_names:
    im_name = random.choice(os.listdir(dir_name + "/" + folder))
    im_file = dir_name + "/" + folder + "/" + im_name
    display(Image(filename=im_file))
~~~
![png]({{ site.baseurl }}/images/2016031901.png)

### Comment
Before I get to Problem 1 I have spent a lot of time download the notMNIST_large due to low RAM I have given to my VM that run the docker container.

For the problem part, it teaches us on using `display(Image(filename=im_file))` which is a very useful function of showing image file on Jupyter Notebook.
