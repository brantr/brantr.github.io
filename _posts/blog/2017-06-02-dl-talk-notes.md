---
layout: post
categories: blog
title: UCSC Deep Learning SCIPP Seminar Notes
use_math: true
---

* Table of Contents
{:toc}


# Deep Learning Seminar Notes

## Introduction

* Seymour Papert 1966 [Summer Vision Project](http://dspace.mit.edu/handle/1721.1/6125)
    -- goal was object identification
* Rules for everyday problems are difficult to write down.
* Talks are extremely difficult.

* Machine learning applications
  -- machine translation
  -- face recognition
  -- road hazard detection
  -- syntax parsing
  -- object detection
  -- image recognition

* Vision -- Imagenet
  -- Imagenet: A large-scale hierarchical image database
  -- J Deng et al. (2009), from Stanford
  -- academic competition focused on prediction 1000 object classes (1.2M images)

* imagenet 2010
  -- SVM 
* imagenet 20911
  -- SVM
* Imagenet 2012
  -- university of toronoto deep convolutional neural network (hinton?)
  -- won by a large margin
  -- every subsequent entry is a nn.

* fine grain classification, generalization, sensible errors
  -- inception v3 architecture

## Deep learning for vision

* alexnet, supervision
* Imagenet classification with deep convolutional neural networks
* Krizhevsky Sutskever Hinton 2012
* multilayer perceptron trained with back propagation known since the 1980s
* backpropagation applied to handwritten zip code
* winning network contained 60 M parameters
* achieving scale in compute and data is critical
  -- large academic data sets
  -- SIMD hardward (GPUs, SSE instruction sets)

* untangling invariant object recognition DiCarlo and Cox (2007)
* Hierarchical composition of simple mathematical functions
* loosely inspired by visual pathway of the brain

* neuron -- perceptron is a toy model
* Rosenblatt 1958 perceptron
* weighted sum of inputs running through nonlinearity
* one of the best is just a max (0,z)

* NN -> y = f(f(...))
* output of network is a real-valued vectors

* Step 1: probabilistic -- softmax function -- normalize distribution
* Step 2: one-hot encoding.  Correct distribution of 1
* KL divergence -- cross entropy loss
* then compute derivatives of loss based on weights -- gradient descent
* Back propagation
* Rumelhart, Hinton, Williams, McClelland et al. 1986
* Werbos (1974)
* Deep networks operate on ~ 1M dimensions
* optimization is highly non-convex
* [playground.tensorflow.org](playground.tensorflow.org)

## image recognition
* LeCun, Bottou, Bengio, And Haffner (1998)
* [http://yann.lecun.com/exdb/minst/](http://yann.lecun.com/exdb/minst/)
* Gradient based learning applied to document recognition
* number parameters for fully connected system -- grows as pixels on side squared
* iphone camera would need 4 million layers for a single layer
* exploit symmetries
 - translation, cropping, dilation, contrast, rotation, scale, brightness
* Ruderman and Bialek (1994) Statistics of natural images: scaling in the woods
* Simoncelli and Olshausen (2001) Natural image statistics and neural representation
* translation invariance -> convolution
* [https://docs.gimp.org/en/plug-in-convmatrix.html](https://docs.gimp.org/en/plug-in-convmatrix.html)
* Subsitute convolutional layer -- model parameters roughly independent of the size of the image
* input and output depth are arbitrary parameters and not equal
* neural networks operate with depths up to 1024
* LeCun et al. 1989 -- two convolutional layers
* Krizhevsky et al. 2012 -- convolutions and fully connected layers

## progress
* 2012 supervision 16.4% error
* karpathy 2014 5.1% (human)
* 2015 inception 3 -- 3.6%
* 2015 resnet 1st 3.6%
* 2016 inception-resnet 3.1%
* best models are of order a thousand layers

* szegedy et al. 2016
* he zhang ren sun 2015
* szegedy 2015
* ioff and szegedy 2015
* karpathy 2014
* simonyan and zisserman 
* inception -- parallel pathways with multiscale filters


## advances in neural networks
* nonlinearities: example of batch normalization
  - covariate shifts are problematic in machine learning
  - blog.bigml.com
  - covariate shifts must be mitigated through domain adaptation
  - input and training and test data have different distributions
  - how to you maintain -- Ioffe and Szegedy 2015 -- Batch Normalization: reduce internal covariate shifts
  - Goodfellow et al. 2013
  - normalize the activiations within a mini-batch
  - learn the moments as a parameter of the network
  - learn the mean and variance of each layer as parameters
  - perceptron y = f(BatchNorm(\Sum w_i x_i))
  - stabalize hidden layer activations
  - CNNs train faster with fewer data samples
  - employ faster learning rates and less network regularizations

* understanding: example of gradient propagation
  - for training a network -- focused on claculating gradients on parameters
  - but how does objectives change based on images 
  - weight vs. image space
  - which pixels elicit a large activation values within a layer?
  - Zeiler and Fergus (@013) -- Visualizing and Understanding Convolutional Networks
  - [http://mscoco.org](http://mscoco.org)
  - what happens if we distort the image
  - what if we used the wrong image
  - Mordvintsev Olah and Tyka (2015) -- Inceptionism: Going Deeper into Neural Networks
  - What pixels distort and image into the "dog"
  - [http://googleresearch.blogspot.com/2015/06/inceptionism-going-deeper-into-neural.html](http://googleresearch.blogspot.com/2015/06/inceptionism-going-deeper-into-neural.html)
  - A Neural Algorithm of Artistic Style -- Gatys, Ecker, Bethge (2015)
  - [https://github.com/kaishengtai/neuralart](https://github.com/kaishengtai/neuralart)
  - Goodfellow, Shlens, And Szegedy (2015) -- explaining and harnessing adversarial examples
  - Szegedy et al. (2014) -- intriguing properties of neural networks
  - add images to see what can fool the network
  - robust across trained networks, architectures, and other machine learnings
  - network operates in different perceptual space

## Conclusions
* [cs231n.github.io/convolutional-networks/](cs231n.github.io/convolutional-networks/) 
* [www.tensoflow.org](www.tensorflog.org)
* [g.co/brainresidency](g.co/brainresidency)
* Applicants in all areas 