---
title: "Optimization Algorithms"
excerpt_separator: "<!--more-->"
categories:
  - Educational
tags:
  - Deep Learning
---
So.. do I use vanilla SGD? SGD with momentum? Nesterov? RMSProp?? Adagrad? Adadelta? Adam?!? lookahead??

I am new to this deep learning business and after days of googling, the only answer to this question I have is to try them all and see what works best, if thats too daunting then __just use Adam__.

The problem I have is that I can't find any theoretical basis for comparing optimization algorithms. There exist a lot of benchmarks and empirical comparisons but pretty much all of them can be neglected by saying they didnt use the right hyperparameters. This leads me to question how exactly do we even rank optimizers? What should be the criterion or "metrics" which we analyze theoretically inorder to establish some kind of hierarchy of optimizers. The first things that come to mind are:
- rate of convergence
- generalizability

Then we can argue that the amount of compute required should also factor in, the number of hyperparameters they require to be tuned should also be included etc.


