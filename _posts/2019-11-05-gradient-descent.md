---
layout: post
title: Gradient Descent
description: Gradient Descent
date: 2019-11-02
author: Saeid Amiri
published: true
tags: Gradient-Descent Newton-Raphson
categories: Algorithm
comments: false
---

## Optimization algorithem
Python is equipped with strong tools for the repeat of some commands or produce sequence number.  

## Contents
- [Newton-Raphson](#newton-raphson)
- [Gradient Descent](#gradient-descent)


## Newton-Raphson method
The Newton-Raphson algorithm is one of old iterative algorithm to approximately find the roots of a real-valued function;
![E_0=mc^2](https://latex.codecogs.com/svg.latex?f(x)=0).
The idea behind of it is based on the simple linear approximation.
Given `x_s`, a starting point, we get closer to the root of function by solving  
![E_0=mc^2](https://latex.codecogs.com/svg.latex?x_{n+1}=x_n-%20\frac{f(x_n)}{\partial%20f(x_{n})}).

The simple and plain algorithm of Newton-Raphosn is given in the below

![picture](https://raw.githubusercontent.com/saeidamiri1/pythonseum/master/public/image/Figure-2019-11-05-newton-raphson-algorithm.png)


Since we should run the iteration for many time; it is better to replace `for` with `while` loop. In the below, we present the algorithm in Python. 

To write the algorithm in code, we consider[E_0=mc^2](https://latex.codecogs.com/svg.latex?f(x)=x^4-3x^2+2) that is also used in [Wikipedia](https://en.wikipedia.org/wiki/Gradient_descent).


Define the function
```
def f(x):
    return x**4 - 3 * x**3+2
def df(x):
    return 4 * x**3 - 9 * x**2
```

To see the minimum of the function, plot it: 

```
from matplotlib import pyplot as plt
import numpy as np 
x_ran_0 = np.linspace(-7,7,100) 
plt.plot(x_ran_0 ,f(x_ran_0))
plt.xlabel('x')
plt.ylabel('f(x)')
plt.show(block=False)
```
 
![picture](https://raw.githubusercontent.com/saeidamiri1/pythonseum/master/public/image/Figure-2019-11-05-gradient-descent-1.png)


To see how the algorithm works, we can add plot the gradients along running the iterations:

```
import matplotlib as mpl

x_s = -4 # Starting point
cur_x = x_s
diff_cur_prev= 1
precision = 0.001
max_ite = 1000  #Maximum number of iterations

#Choose different colors for each gradient
colors = mpl.cm.autumn(np.linspace(0,5,max_ite)) 

plt.plot(x_ran_0 ,f(x_ran_0)) # plot again the  f(x)

i= 1
while diff_cur_prev > precision:
    #Plot the points 
    plt.scatter(cur_x, f(cur_x), color='black', s=10, zorder=2);
    plt.scatter(cur_x, f(cur_x), color='white', s=5, zorder=2)  
    x_ran_1= np.linspace(cur_x-5,cur_x+5,10)
    plt.plot(x_ran_1, (df(cur_x) * (x_ran_1 - cur_x)) + f(cur_x), color=colors[i], zorder=1)
    prev_x = cur_x
    cur_x += -f(prev_x) / df(prev_x)
    diff_cur_prev = abs(cur_x - prev_x)
    print("Run: %d, Current: %f, Previous: %f, Different: %f" % (i, cur_x,prev_x,diff_cur_prev))
    i+= 1

plt.xlim([-10,10])
plt.xlabel('x')
plt.ylabel('f(x)')
plt.show(block=False)
```

![picture](https://raw.githubusercontent.com/saeidamiri1/pythonseum/master/public/image/Figure-2019-11-05-gradient-descent-2.png)

## Gradient Descent
Gradient Descent is a numerical method to find the minimum value of a differentiable function.  The local minimum can be obtained using solving 

![E_0=mc^2](https://latex.codecogs.com/svg.latex?x_{n+1}=x_n-\gamma%20\frac{\partial%20f}{\partial%20x_{n}})

where ![E_0=mc^2](https://latex.codecogs.com/svg.latex?\gamma) is called the step size or learning rate, see [Wikipedia](https://en.wikipedia.org/wiki/Gradient_descent).  Obviously, the criterion function is different from the Newton-Raphson Algorithm. 

To write a simple code to find the minimum using the Gradient Descent consider ![E_0=mc^2](https://latex.codecogs.com/svg.latex?f(x)=x^4-3x^2+2) that is already used for exoalning the Newton-Raphosn. 


The plot of gradient can be obtained using running the following script:
```
import matplotlib as mpl

x_s = -4 # Starting point
cur_x = x_s
diff_cur_prev= 1
gamma = 0.001 
precision = 0.001
max_ite = 1000  #Maximum number of iterations

#Choose different colors for each gradient
colors = mpl.cm.autumn(np.linspace(0,5,max_ite)) 

plt.plot(x_ran_0 ,f(x_ran_0)) # plot again the  f(x)

i= 1
while diff_cur_prev > precision:
    #Plot the points 
    plt.scatter(cur_x, f(cur_x), color='black', s=10, zorder=2);
    plt.scatter(cur_x, f(cur_x), color='white', s=5, zorder=2)  
    x_ran_1= np.linspace(cur_x-5,cur_x+5,10)
    plt.plot(x_ran_1, (df(cur_x) * (x_ran_1 - cur_x)) + f(cur_x), color=colors[i], zorder=1)
    prev_x = cur_x
    cur_x += -gamma * df(prev_x)
    diff_cur_prev = abs(cur_x - prev_x)
    print("Run: %d, Current: %f, Previous: %f, Different: %f" % (i, cur_x,prev_x,diff_cur_prev))
    i+= 1

plt.xlim([-10,10])
plt.xlabel('x')
plt.ylabel('f(x)')
plt.show(block=False)
```

![picture](https://raw.githubusercontent.com/saeidamiri1/pythonseum/master/public/image/Figure-2019-11-05-gradient-descent-3.png)


**[⬆ back to top](#contents)**
### License
Copyright (c) 2019 Saeid Amiri