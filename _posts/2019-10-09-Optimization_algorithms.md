---
title: "Optimization Algorithms"
excerpt_separator: "<!--more-->"
categories:
  - Educational
tags:
  - Deep Learning
  - Notes
---

This is just a collection of improvements on the classical gradient descent algorithm from neural nets where
the grads during backprop are computed all at once by vectorization. This classic algorithm is named Batch gradient descent.

For extremely large datasets it can be slow to update the gradient only once per pass through the entire training set
(i.e: 1 update per epoch). In order to increase the update frequency of the gradient we can divide our training set into 
mini batches and update the gradient with each pass through a minibatch. For example if i have a training set of 1000 elements
I can divide it into 100 minibatches with 10 elements each. This will result in the grad being updated 100 times per epoch. 
With an added downside of there being more fluctuations or oscillations of the cost function since now we will be updating the
grad based on small portions of the training set. The size of the minibatch is somewhat arbitrary but there are 2 tradeoffs to 
consider:
1. Too small a minibatch means we no longer have the advantage of vectorized implementations, and for a minibatch of size 1 we 
are basically using stochastic gradient descent. This has a very high variance in the grad with each consecutive update.
2. Too large a minibatch means we will have to do a lot of computation before the gradient gets updated.

Inorder to fix the problem of high variance in the gradients and to still take advantage of faster gradient updates with 
minibatches we can use some smoothing techniques like:
- Momentum 
- RMSprop
- [Adam](https://arxiv.org/pdf/1412.6980.pdf)

These techniques use something called exponential weighted averages. Where the next value for a variable V is not straight up considered to be the new value. Instead we take into account the previous value and have a weight of around 0.9 for it and a weight of 0.1 for the new value. This means our updating procedure is not very responsive to changes , we signify this with a parameter Beta.


![eqs](https://i.stack.imgur.com/p8oDT.jpg)

If we consider values over multiple iterations then we notice that 


- The value of beta can be seen in this way: if its 0.9 then it is like saying we are averaging over the past 10 values. if 
its 0.999 then its like saying we are averaging over the past 1000 values to update the current value. the larger the value is the more weight we assign to previous values. This is better visualized by calculating a series of values from V_0 to V_5 or 6 and observing that all the previously calculated values are being included in the V_5 calculation:


$$V_0 = 0 $$

$$
V_1 = \beta * V_0 + (1 - \beta) * X_1  \\
V_2 = \beta * V_1 + (1 - \beta) * X_2 \\
V_3 = \beta * V_2 + (1 - \beta) * X_3 \\
V_4 = \beta * V_3 + (1 - \beta) * X_4 \\
V_5 = \beta * V_4 + (1 - \beta) * X_5 \\$$
