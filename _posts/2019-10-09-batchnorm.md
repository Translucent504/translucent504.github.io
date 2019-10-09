---
title: "Post: Batch normalization"
excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - Deep Learning
  - Notes
---

# Batch normalization
- Purpose: Speed up the learning of the parameters w,b of the hidden layers
- Idea: Normalize the outputs of neurons the same way initial inputs are normalized for increased efficiency

This makes the cost function more 'symmetric' rather than being skewed towards some feature that is like 10000 times larger 
that the other inputs.

There is debate whether to normalize z or a. i,e whether to normalize before the output of the activation function or after.
Usually it is done before the activation function so we normalize z.

When we usually normalize the x inputs we set their mean and variance to 0 and 1 by :
> ![x-normalize-equation](https://latex.codecogs.com/gif.latex?%5Coverline%7Bx%7D%20%3D%20%5Cfrac%7Bx-%5Cmu%7D%7B%5Csqrt%7B%5Csigma%5E%7B2%7D%7D%7D)

![mean](https://latex.codecogs.com/gif.latex?%5Cmu%20%3A%20mean)

![variance](https://latex.codecogs.com/gif.latex?%5Csigma%5E%7B2%7D%20%3A%20variance)

For z we use the same normalization with a small epsilon is added to prevent division by 0 errors:
> ![z-normalize-equation](https://latex.codecogs.com/gif.latex?%5Coverline%7Bz%7D%20%3D%20%5Cfrac%7Bz-%5Cmu%7D%7B%5Csqrt%7B%5Csigma%5E%7B2%7D&plus;%5Cepsilon%7D%7D)


But we dont want all of our neurons to have a (mean, variance) of (0, 1) since based on
the activation function this will force the outputs to be clustered in a very small region which for a function like sigmoid 
will lie in the linear region for which we are going to have a new equation:
> ![z-tilda](https://latex.codecogs.com/gif.latex?%5Clarge%20%5Ctilde%7Bz%7D%20%3D%20%5Cgamma%20%5Cbar%7Bz%7D%20&plus;%20%5Cbeta)

where we have gamma and beta as new learnable parameters as part of the neural net. This allows us to set the mean and variance 
of z.

# Why does it work?

first reason as stated in the beginning , it makes the range of values of the hidden units smaller. (dont have some units producing outputs from 1-10 while others produce from 1000-100000 etc. 
