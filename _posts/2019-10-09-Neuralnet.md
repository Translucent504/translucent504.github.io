---
title: "Post: Neural Nets"
excerpt_separator: "<!--more-->"
categories:
  - Blog
tags:
  - Deep Learning
  - Notes
---

# Wtf is a Neural net and how do all the computations work??? abay ooo mere apnay desi bois ke liye hai yeh zada jasoosi na karo
A neural net is a jugaari way to approximate a function.

## What do I mean by function?
A function takes in a set of inputs and gives a certain output.
consider a function f(x) = x + 2
If i give this function an input of [1,2,3,4,5] i will get the outputs [3,4,5,6,7]

---

Now imagine if just had these inputs and outputs and I did not know what the function actually was..
How would i go about approximating the original function f(x)..
well i would guess that my approximate function g depends on the input x and i will show this dependency with a 'weight'
so i could say g(x) = w * x this however would restrict me to functions that are directly proportional to my input i.e 
only functions that pass through the origin so i say lets add a "bias" or "intercept" term as well to cover larger ground.
so i guess a generic linear function g(x) = w * x + b

---

Now i start an exhaustive process where i fix the value of b to something like 1 or 0 or 5 or whatever. and i keep varying
the value of w from -5 to +5. Now note that i still have the initial 'dataset' of inputs and  outputs : [1,2,3,4,5] -> [3,4,5,6,7]
so i input 1 , 2 ,3 ,4 ,5 inplace of x in my g(x) and i see what the output is...
I need some way of measuring whether my function is even doing a good job or not.. for this purpose i will take the help of an
'Error value' or a "Cost value". which basically has the purpose to give me an idea about if I input to my function 4, i know the expected
output from the dataset is 6, how close is my function to the expected output of 6? 

## How to calculate an Error value?
I could simply say well I'm going to take the difference in my function's output g(x) and the expected output from the 'dataset'.
so i define my 
- Error = g(x) - expected output


the problem with this definition is that I want to set a standard i.e if the value of Error is large then my function is doing bad
and if the value of error is small then my function is doing great. Now consider if i was to set my function as:
- g(x) = -5 * x - 1


on the input x = 1 the expected output is 3
my function gives the output -6 , the Error value will come out to be 
- Error = (-6 - 3) = -9 


-9 is a very small value, and doesnt reflect the fact that my function is actually doing poorly. so I learn that i need to avoid negative
error values. Another problem is that when i go to see the performance of my function as a whole on the entire 'dataset' i go about
calculating the error value for each input and output pair and I sum all the values of the error together, the negative values are going
to give me a wrong result.
To fix this problem I can consider a squared error function
- Error = ( g(x) - expected output ) ^ 2


Alright so this new error function is always going to give me a positive answer and solves the negative values ruining the sum of errors problem too.
Now we can be fancy and we can call the output of our function 'g' the predicted output. So I can say that a measure of the
performance of my approximate function can be calculated by summing the Error value I get from comparing my predicted output to the expected output of the dataset.
- Error = SUM [ ( g(x) - expected output ) ^ 2 ]


Now this whole idea of fitting or approximating a function to some data is very well studied and we can find better derived
ways or mathematical recipes if we do some internet searching. under the name of Regression , in our case Linear regression.
This idea of tweaking some parameter and checking the cost function seems to be a good idea but in practice we need some solid method to actually tweak the parameters in a way that is surely going to reduce the cost. We do this by means of a simple approach called gradient descent. The idea is to calculate the gradient of our cost function. The gradient basically tells you how the cost function changes as we change the parameters, more precisely the grad shows the direction in which we should tweak the parameters to result in the maximum INCREASE in the cost function so what we do is we calculate the grad and we update the parameters in the OPPOSITE direction to the grad. This is seen in backprop. The mathematical tool which we use to calculate these grads is calculus (derivatives). However there is a problem. all functions arent simple and smooth and there are many functions that have a lot of bumps and kinks. if our cost function turns out to be one of the BAD functions we will be out of luck since our algorithm isnt going to work well for those cases. We classify nice functions as CONVEX functions so we would hope that our cost function is also convex ( only one lowest point with no silly bumps or kinks). Our squared error function works well for the case of linear regression but for the cases where we may want to try something else like Logistic regression ( classification like yes or no type output) we notice that our cost function does not look convex. for that purpose we have a new cost function which we will call a Log loss function or to be fancy the cross entropy loss function:

![cross entropy](https://ml-cheatsheet.readthedocs.io/en/latest/_images/logistic_cost_function_joined.png)

Now this function satisfies our need for a cost function that is convex and works for the case where we want discrete or non continous classification rather than linear continous prediction. For the log function we only need to keep in mind the behavior when we get log(0) and when we get log(1)... the log function goes to a very very very negative value like negative infinity when we have Log(0) and Log(1) = 0 with this in mind when we look at our cost function we see that for the case when expected y = 1 and our predicted h = 0. The term on the right side becomes 0 due to the (1 - y) so the cost will be log(0) which means a very very negative value. For the other case where y = 1 and h = 1 we see that its the same case and we get Log(1) and the cost is 0. The same is true for the cases where y = with h =1 and y = 0 with h = 0. if the predicted and expected output is the same we get 0 cost and if they are different we get an extremely negative cost. for which we have the additional minus sign at the back. m in the figure refers to every single example from the data set like for example if i have 5 photos and i mark them whether they have a red ball in them or not. i will have an m = 5. which just represents the size of the dataset. Since we arent just going to run our prediction on a single input we are going to use the entire data set so we take the average cost by summing all the costs from predictions over the dataset and divide it by the size of the dataset i.e ( m )

Consider this now, instead of only tweaking one/two parameters w,b and approximating a linear function, I go about and have 
this idea of approximating much more complex functions. So what i can do is add multiple terms to my original function
and say that it is infact a polynomial 

- g(x) = ax^5 + bx^4 + cx^3 + dx^2 +ex +f

now i can go about and tweak the values of a b c d e f until im satisfied with the error functions result. another way to do
this approximation is to use a neural net. the thing with neural nets is that u can use a very simple linear function
and still be able to approximate crazy complex functions. a neural net is made up of multiple layers of neurons or nodes.
they arent anything special. they just take in a set of inputs and output a single number. its basically a function approximation. The fancy thing here is that even though we are just trying to "LEARN" or approximate a single function, we do this by doing something seemingly pointless which is as following this recipe:

- take an input X, throw it into every neuron of the first "layer" of the neural net.
- take the outputs of all the neurons of the first layer and throw them into every neuron of the second layer.
- take the outputs of all the neurons of the second layer and throw them into every neuron of the third layer.
- and on and on... until you get to the last layer, which you decide arbitrarily. (hyperparameter tuning OoOoO fancy words)
- in ur last layer you have a single neuron which acts as your output. which takes in all the outputs of the previous layer as inputs and outputs a single final answer.
- this final answer is your prediction or approximation.

now how do these neurons or nodes go about generating an output? well they are all small packages of linear regression functions with a (NON LINEARIZERATOR) activation function attached at the end.

## what is the point of attaching an activation function at the end of a neuron?
Since they are already outputting a single number based on all the previous inputs, whats the point of attaching this activation function on top? If we try to get our hands dirty and see what is actually happening without activation functions it gets really obvious:

- consider a very simple neural net with 1 input x, 2 nodes in layer1 and 2 nodes in layer 2 and an output node.

>looks something like this : x -> [o][o] -> [o][o] -> [o] -> output

initial input x => Layer 1 neurons (L1n1,L1n2)
L1n1 takes input x and outputs a single number based on linear regression so we write it as:
- L1n1(x) = L1n1w1 * x + L1n1b

similarly we can write for neuron 2:
- L1n2(x) = L1n2w1 * x + L1n2b

Now consider Layer 2 neurons(L2n1, L2n2)
they take 2 inputs each which we consider i1 and i2 for now:
- L2n1(i1, i2) = L2n1w1 * i1 + L2n1w2 * i2 + L2n1b
- L2n2(i1, i2) = L2n2w1 * i1 + L2n2w2 * i2 + L2n2b

now note that i1 and i2 are actually the outputs of the previous layer so we see
- i1 = L1n1w1 * x + L1n1b
- i2 = L1n2w1 * x + L1n2b

substituting these values into layer 2 equations we see:

- L2n1(i1, i2) = L2n1w1 * ( L1n1w1 * x + L1n1b ) + L2n1w2 * ( L1n2w1 * x + L1n2b ) + L2n1b
- L2n2(i1, i2) = L2n2w1 * ( L1n1w1 * x + L1n1b ) + L2n2w2 * ( L1n2w1 * x + L1n2b ) + L2n2b

you can already see there are some terms common here. moving onto the final layer's neuron which takes in 2 inputs o1 and o2:

- L3n1(o1,o2) = L3n1w1 * o1 + L3n1w2 * o2 + L3n1b

Now we know that o1 and o2 are the ouputs of the 2nd layer i.e L2n1 and L2n2 we can substitute for them:

- L3n1(o1, o2) = L3n1w1 * [L2n1w1 * ( L1n1w1 * x + L1n1b ) + L2n1w2 * ( L1n2w1 * x + L1n2b ) + L2n1b] 
+ L3n1w2 * [L2n2w1 * ( L1n1w1 * x + L1n1b ) + L2n2w2 * ( L1n2w1 * x + L1n2b ) + L2n2b] 
+ L3n1b

from these equations we can start cleaning up with some algebraic manipulation and factoring now.

  L3n1w1 ( L2n1w1L1n1w1x + L2n1w1L1n1b + L2n1w2L1n2w1x + L2n1w2L1n2b + L2n1b) 
+ L3n1w2 ( L2n2w1L1n1w1x + L2n2w1L1n1b + L2n2w2L1n2w1x + L2n2w2L1n2b + L2n2b)
+ L3n1b

= L3n1w1L2n1w1L1n1w1x + L3n1w1L2n1w1L1n1b + L3n1w1L2n1w2L1n2w1x + L3n1w1L2n1w2L1n2b + L3n1w1L2n1b
+ L3n1w2L2n2w1L1n1w1x + L3n1w2L2n2w1L1n1b + L3n1w2L2n2w2L1n2w1x + L3n1w2L2n2w2L1n2b + L3n1w2L2n2b
+ L3n1b

= x * (**L3n1w1L2n1w1L1n1w1 + L3n1w1L2n1w2L1n2w1 + L3n1w2L2n2w1L1n1w1 + L3n1w2L2n2w2L1n2w1**) + *L3n1w1L2n1w1L1n1b + L3n1w1L2n1w2L1n2b + L3n1w1L2n1b + L3n1w2L2n2w1L1n1b + L3n1w2L2n2w2L1n2b + L3n1w2L2n2b + L3n1b*

Notice that all the terms in *italics* just add up to a single constant number C, same for the terms in **bold** which also add up to a constant which we can call B.

so our reduced final answer is:
- L3n1(o1, o2) = x * B + C

In the end of all this mayhem we see that if all the neurons have just this linear regression function output we can at best output a Linear function of x as represented by 
- L3n1(x) = x * B + C
- g(x) = B * x + C

The only functions we can approximate with this sort of a neural network are linear functions, **so a neural net with 1000 layers and 1000 neurons in each layer is the same as a single neuron if they dont have a non linear activation function.**

For this reason we attach an activation function at the end of all the neurons outputs, so they still act as the linear regression balls but also have a non linearity attached to them. Some examples of common activation functions are:

- Sigmoid(z)
- ReLu(z)
- Tanh(z)

# TODO:
- [ ] forward prop
- [x] back prop

# Backprop:
Scene yeh hai ke we need to reduce the Error/cost function for which we use gradient descent for which we need to travel in the direction opposite to the GRADIENT. So we need a way to calculate the gradient of the Cost function with respect to all the parameters and then update them all according to the gradient. Inorder to calculate the gradient we use the **CHAIN RULE**
the idea is that since the final output is a function of the preceeding neuron which is a function of the preceeding neuron and so on... if we know the partial derivative of the cost function with respect to the output layer then by the chain rule we can work our way back through the neural network calculating partial derivatives at each step.

## Concretely:
Consider a neural net with this structure:
>X -> (Linear->ReLu) A1/Z1/W1-> (Linear->ReLu) A2/Z2/W2 -> sigmoid A3/Z3/W3 -> output ( A3 is the output )

Once we know the cost J = 10
The cost is a function of the output i.e A3
Also it is good to refer to this table


| Var| Function    |
|----|-------------|
| Z1 | W1 * X + b1 |
| A1 | ReLu(Z1)    |
| Z2 | W2 * A1 + b2|
| A2 | ReLu(Z2)    |
| Z3 | W3 * A2 + b3|
| A3 | Sigmoid(Z3) |

So if I know J is directly a function of A3 based on my choice of error function. I can directly calculate 
- dJ/dA3

Since i know A3 is a function of Z3 by the chain rule i can calculate
- dJ/dZ3 = (dJ/dA3) * (dA3/dZ3)
- dJ/dZ3 = A3 - Y
Now that i have dJ/dZ3 and i know that W3 and b3 are functions of Z3 i can use the chainrule again:

- dJ/dW3 = (dJ/dZ3) * (dZ3/dW3)
- dJ/dW3 = (dJ/dZ3) * (A2)
- dJ/db3 = (dJ/dZ3) * (dZ3/db3)
- dJ/db3 = (dJ/dZ3) * (1)
- **Shorthand for dJ/dA2 is dA2 and so on...**
- dA2 = dZ3 * d(Z3)/d(A2)
- dA2 = dZ3 * W3
- dZ2 = dA2 * d(A2)/d(Z2)
- dZ2 = dA2 * (1 or 0)[depending on whether A2 is > 0 or not because ReLu gradient = 1 if x>0 and 0 otherwise.]
- dW2 = dZ2 * d(Z2)/d(W2)
- dW2 = dZ2 * A1
- db2 = dZ2 * 1
- dA1 = dZ2 * d(Z2)/d(A1)
- dA1 = dZ2 * W2
- dZ1 = dA1 * (int(A1>0))
- dW1 = dZ1 * X
- db1 = dZ1 * 1




