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

## [A Guide to TF Layers: Building a Convolutional Neural Network](https://www.tensorflow.org/tutorials/layers)  

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

** In `main()`, we need to define the dataset.  We select the `mnist.train.images` to get the training dataset, and load the labels as an array.  We then define a test or evaluation dataset, which is `mnist.test.images` and its corresponding labels as an array.

** The `tf.estimator.Estimator()` function is given the `cnn_model_fn` and a model output directory.  The classifier is then trained via `mnist_classifier.train()` and then evaluated using `mnist_classifier.evaluate()`.

## [Deep Convolutional Neural Networks](https://www.tensorflow.org/tutorials/deep_cnn)  

** This tutorial covers classification of the [CIFAR-10](https://www.cs.toronto.edu/~kriz/cifar.html) data set.  The model is based on [AlexNet](https://papers.nips.cc/paper/4824-imagenet-classification-with-deep-convolutional-neural-networks.pdf).

** The CIFAR-10 data is based on fixed length binary information, and there is a `tf.FixedLengthRecordReader`.

** [Image distortion and augmentation](https://www.tensorflow.org/api_guides/python/image) is applied.

** The model adds [local response normalization](https://www.tensorflow.org/api_docs/python/tf/nn/local_response_normalization) as a step. This normalizes individual images by taking a weighted, squared sum of nearby images in the array.

** The model splits training and evaluation into separate scripts `cifar10_train.py` and `cifar10_eval.py`.

** As an exercise, they suggest downloading the [Street View House Numbers](http://ufldl.stanford.edu/housenumbers/) database and re-running the AlexNet model. This requires doing some reading with MatLab, so on the back burner for the time being.

## [How to Retrain an Image Classifier for New Categories](https://www.tensorflow.org/tutorials/image_retraining)  

This retrains ImageNet to classify flowers.  First the [flower images](http://download.tensorflow.org/example_images/flower_photos.tgz) and the [retraining example](https://github.com/tensorflow/hub/raw/r0.1/examples/image_retraining/retrain.py) are downloaded.  The retraining is started using `python retrain.py --image_dir ~/flower_photo`, this creates the bottlenecks that help apply ImageNet to a new classification set.  The code then procedes to train and estimate accuracy.  The tutorial also shows how to use [TensorBoard](https://github.com/tensorflow/tensorboard) (e.g., `tensorboard --logdir /tmp/retrain_logs`).  The `label_image.py` [script](https://github.com/tensorflow/tensorflow/raw/master/tensorflow/examples/label_image/label_image.py) provides a starting point for using a retrained ImageNet for classification. One can also specify the dimensions of the images:

```python
python label_image.py \
--graph=/tmp/output_graph.pb --labels=/tmp/output_labels.txt \
--input_layer=Placeholder \
--output_layer=final_result \
--input_height=224 --input_width=224 \
--image=$HOME/flower_photos/daisy/21652746_cc379e0eea_m.jpg
```

## [Image Recognition](https://www.tensorflow.org/tutorials/image_recognition)  

This tutorial teaches you to use [Inception-V3](https://arxiv.org/abs/1512.00567) to perform image classification on [ImageNet](http://image-net.org/). The example `classify_image.py` downloads a pre-trained Inception-V3 and then classifies an image of a panda.

## Other Information
** [Linear Rectifier](https://en.wikipedia.org/wiki/Rectifier_(neural_networks)).  
** [Sigmoid](https://en.wikipedia.org/wiki/Sigmoid_function)  
** [Tensorflow w/ CUDA Info](https://www.nvidia.com/en-us/data-center/gpu-accelerated-applications/tensorflow/)
