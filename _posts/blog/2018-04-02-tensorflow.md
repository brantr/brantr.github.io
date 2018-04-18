---
layout: post
categories: blog
title: Tensorflow Tutorials
use_math: true
---

* Table of Contents
{:toc}

## GPU-Accelerated Tensorflow

[NVIDIA + Tensorflow](https://www.nvidia.com/en-us/data-center/gpu-accelerated-applications/tensorflow/)

## A list of Tensorflow tutorials

[Tensorflow Tutorials](https://www.tensorflow.org/tutorials)  

* [A Guide to TF Layers: Building a Convolutional Neural Network](https://www.tensorflow.org/tutorials/layers)  

This tutorial covers [MNIST](http://yann.lecun.com/exdb/mnist) and shows how to build a CNN-based classification model. It introduces [ReLU](https://en.wikipedia.org/wiki/Rectifier_(neural_networks)) activation functions and [pooling layers](https://en.wikipedia.org/wiki/Convolutional_neural_network#Pooling_layer). The tutorial also introduces [softmax](https://en.wikipedia.org/wiki/Softmax_function) activation functions. It references the [Stanford CS23](https://cs231n.github.io/convolutional-networks) course on convolutional neural networks. It introduces a [loss function](https://en.wikipedia.org/wiki/Loss_function) and the [cross entropy](https://en.wikipedia.org/wiki/Cross_entropy) function. It also introduces [one-hot encoding](https://www.quora.com/What-is-one-hot-encoding-and-when-is-it-used-in-data-science) and [stochastic gradient descent](https://en.wikipedia.org/wiki/Stochastic_gradient_descent).

** First we define the model function, which returns an estimator.  It takes as arguments the data, labels, and a mode (e.g., train, eval, predict).

** `layers` module expects tensors of size `[batch_size, image_width, image_height, channels]`. `batch_size` is number of images for training and `channels` is, e.g., 3 for RGB or 1 for BW. We can use `tf.reshape()` to make this tensor.

** `conv2d()` module receives the input layer, and then the output size depends on padding (e.g., `padding=same` zero pads to maintain the image size). The output `channels` of `conv2d()` will be the number of `filters` times the number of input `channels`, times the size of the images. An activation function has to be indicated (e.g., `tf.nn.relu`).

** `max_pooling2d()` receives the convolution, and uses `pool_size=[n,m]` to reduce the size by `n` and `m` in each direction provided the `strides=n`. For instance, max pooling 2x2 reduces a 28x28 image to 14x14.

** `tf.reshape()` can be used to take the output from `conv2d()` and `max_pooling2d()` and make it `batch_size x ` a 1D array. That
can be input into `tf.layers.dense()`.

** `tf.layers.dense()` takes a flattened input tensor, and you specify the number of neurons with `units`. Note that `units` does not need to equal the number of array elements in the flattend input tensor. An activation function must be specified (e.g., `tf.nn.relu`).

** `tf.layers.dropout()` applies dropout regularization, with `rate` indicating the percentage of neuron outputs that are randomly dropped.

** `training` specifies if we are training, which can be passed by the `tf.estimator`.

** The output of `dropout()` is `batch_size x units`.

** The `logits` layer is another `dropout`, but with an output `units=10` for `mnist`.

** Predicted class can be found using `tf.argmax()`.

** The probabilities can be determined using `tf.nn.softmax()`.

** These predictions are then zipped and returned if in prediction mode.

** Otherwise, a loss function is computed -- instead of `one_hot` tutorial now uses `sparse_softmax_cross_entropy` directly on input labels and output logits.

** If training, then define a `tf.train.GradientDescentOptimizer` with an input learning rate (e.g., 0.001). Pass the loss function output to the optimizer. Then return the estimator.

** If evaluating, just compute the accuracy from `tf.metrics.accuracy` and return the estimator.

** At this point, the model is defined.  We then have to define a `main()` function to run the model on the data.

[Deep Convolutional Neural Networks](https://www.tensorflow.org/tutorials/deep_cnn)  
[How to Retrain an Image Classifier for New Categories](https://www.tensorflow.org/tutorials/image_retraining)  
[Image Recognition](https://www.tensorflow.org/tutorials/image_recognition)  
[Linear Rectifier]()  
[Sigmoid](https://en.wikipedia.org/wiki/Sigmoid_function)  

[Tensorflow w/ CUDA Info](https://www.nvidia.com/en-us/data-center/gpu-accelerated-applications/tensorflow/)
