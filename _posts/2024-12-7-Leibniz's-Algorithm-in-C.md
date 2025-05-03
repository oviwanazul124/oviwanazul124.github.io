---
title: Leibniz's Algorithm in C
date: 2024-12-7 17:42:10 +0100
categories: [Programming]
tags: [c, Tutorial, English]
description: Short tutorial on how to develop Leibniz's algorithm in C.
math: true
lang: en
translations:
  ja: /ja/leibnizs-algorithm-in-c/
  en: /posts/Leibniz's-Algorithm-in-C/
  es: /es/leibnizs-algorithm-in-c/

---

## Brieft Introduction

To develop Leibniz’s algorithm in C we must first know what the algorithm is based on. Here is the mathematical formula of the algorithm / series

$$\sum_{n=0}^\infty\frac{(-1)^n}{2n + 1} = \frac{\pi}{4}$$

## Explaining Process

### Including Libraries

First we need to import the following libraries.

```c
#include <stdio.h>
#include <math.h>
```

> Make sure you import them or you will have problems in the future.
{: .prompt-danger }

The stdio library is the standart library of C, while 'math.h' is the library that we will use to take care of the more advanced mathematics (If you decide to use the other method explained above, you do not need to import this library).

### Including all the variables

The next thing we have to do is to set the variables which will be **iter**, which will be in charge of showing the different iterations that we will perform, then there will also be **cont** which will be in charge of counting each iteration performed that the user originally entered and finally we will add a **pi** which will include a series of digits of pi in order to calculate the error that the series can produce.

```c
int iter;
int cont = 0;
float pi = 3.141592653589793;
```

### The functions

We will use two functions in this program the first one will be a function called **introduction()** this will be in charge of welcoming the user and introducing the numbers, the other function will be the one that calculates the series, we will call it **series()**. 

```c
// Global Functions

void introduction();
void serie();
```

## Introduction function

This function is in charge of requesting the number of iterations for which pi is to be calculated, after which it is stored in the variable created in [including all the variables](#including-all-the-variables).After this it checks if it is 0 or negative because if this is the case it would give errors so if it happens it would resort again to ask the user for a number of iterations and finally to the [function series](#serie-function).

```c

printf("Please enter the number of iterations you want to perform. \n");
scanf("%i", &iter);

    while(iter <= 0){
        printf("It seem you have entered a number that is less than or equal to 0, please enter a positive number. \n");
        scanf("%i", &iter);
    }
    serie();
```


> In case you didn't know, ‘\n’ allows the following message to appear on the next line of the terminal.
{: .prompt-info }


## Serie function
Next we use a while that will run until the variable **cont** is greater than the proposed number of iterations. The next thing we will do is create a variable **d** this will be in charge of the fraction of the [formula](#brieft-introduction) that we have shown at the beginning, then we define another variable called **result** , this will be in charge of adding the result obtained by the fraction (we multiply it by 4 because otherwise it would give us pi/4 not pi).
```c
 printf("iter, error, result \n");
    while(cont < iter){
        double d;
        d = ((powf(-1, cont)) / (2*cont + 1));
        double result;
        result += (d*4);
        cont += 1;
        double error = fabs(((pi - result) / pi) * 100);
        printf("%4i, err:%4e, %4lf \n", cont, error, result);
    }
  cont = 0;
  introduccion();
```

> In case you didn't know, we use 'double' because C has a limit to the number of bytes that can be stored in a single variable, so if we don't use it, it can cause unwanted calculation errors.
{: .prompt-info }


## Final Code

The final code can be found on my [github](https://github.com/oviwanazul124/Leibniz-s-Algorithm-in-C/blob/main/main.c) page.
