---
layout: post
title: Tensorflow (Machine learning toolset Open Source by Google)
tags: [Machine-learning, Python, Tensorflow]
---

![tensors-flowing]({{ site.baseurl }}/images/2015111400.gif "tensors-flowing")

### Tensorflow

On 10th November, I saw the news that [Google open sourced Tensorflow](http://www.wired.com/2015/11/google-open-sources-its-artificial-intelligence-engine/?mbid=social_fb). As a programmer that is passionate towards AI, this is a thing that I must try out.

### Setup
FYI, setup instruction can be found at [here](www.tensorflow.org/get_started/os_setup.md).

### Tensorflow with mnist

Put the file at `/home/vagrant/notebook/`

- Download [fully_connected_feed.py](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/g3doc/tutorials/mnist/fully_connected_feed.py)
  - replace `from tensorflow.g3doc.tutorials.mnist import input_data` to `import input_data`
  - replace `from tensorflow.g3doc.tutorials.mnist import input_data` to `import mnist`
- Download [input_data.py](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/g3doc/tutorials/mnist/input_data.py)
- Download [mnist.py](https://github.com/tensorflow/tensorflow/tree/master/tensorflow/g3doc/tutorials/mnist/mnist.py)

Execute `python fully_connected_feed.py`, it should run and give you the result like this

```
Step 1000: loss = 0.40 (0.007 sec)
Step 1100: loss = 0.52 (0.087 sec)
Step 1200: loss = 0.46 (0.005 sec)
Step 1300: loss = 0.49 (0.005 sec)
Step 1400: loss = 0.48 (0.006 sec)
Step 1500: loss = 0.37 (0.029 sec)
Step 1600: loss = 0.45 (0.005 sec)
Step 1700: loss = 0.40 (0.005 sec)
Step 1800: loss = 0.39 (0.005 sec)
Step 1900: loss = 0.44 (0.006 sec)
Training Data Eval:
  Num examples: 55000  Num correct: 49219  Precision @ 1: 0.8949
Validation Data Eval:
  Num examples: 5000  Num correct: 4508  Precision @ 1: 0.9016
Test Data Eval:
  Num examples: 10000  Num correct: 8978  Precision @ 1: 0.8978
```

### Graph visualization

Now run `tensorboard --logdir=/home/vagrant/notebook/data`, open browser at localhost:6006 to view the graph. You should be able to see something like this:

![tensorboard]({{ site.baseurl }}/images/2015111401.png "tensorboard")

### My Review

Not really standout from torch/caffe/etc, I thought it has the ability to drag and drop modify code like Pentaho, however it only has the ability to view the summary graph.

- Overall - Good to use.
- Surprising me? Not.
