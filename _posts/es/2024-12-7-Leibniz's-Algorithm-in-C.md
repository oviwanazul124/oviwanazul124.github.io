---
title: Algoritmo de Leibniz en C
date: 2024-12-7 17:42:10 +0100
categories: [Coding]
tags:
  - C
  - Tutorial
  - Spanish

excerpt: Un pequeño tutorial de como implementar el algoritmo de Leibniz's en C

toc: true
toc_sticky: true
use_math: true

language: es
ref: leibniz-algorithm
lang_en: /en/leibniz-algorithm
lang_es: /es/leibniz-algorithm
lang_ja: /jp/leibniz-algorithm
permalink: /es/leibniz-algorithm
---

## Breve introducción

Para implementar el algoritmo de Leibniz en C primero debemos conocer el algoritmo en el que se basa. Aquí podemos observar la formula utilizada:

$$\sum_{n=0}^\infty\frac{(-1)^n}{2n + 1} = \frac{\pi}{4}$$

## Explicando el proceso

### Incluyendo la libreria

Primero debemos importar las siguientes librerias

```c
#include <stdio.h>
#include <math.h>
```

Asegurate de importar dichas librerias si no tendrás fallos en el futuro.
{: .notice--danger }

La librería de stdio es la librería estandar de C, mientras que 'math.h' es una librería para encargarnos de los metodos más complejos de las matematicas (Si prefieres programarlo a mano, no es necesario de utilizar dicha librería).

### Incluyendo las variables

Lo siguiente que vamos a hacer es crear la variable **iter**, la cual se encargará de mostrar los diferentes ciclos que se han realizados, también crearemos otra variable llamada **cont** que se encargará de contar el ciclo actual y sumarlo, finalmente crearemos una última variable llamada **pi** que incluirá la serie de los digitos de pi, para calcular el error que ha producido la serie.

```c
int iter;
int cont = 0;
float pi = 3.141592653589793;
```

### Las funciones

Las funcionas que vamos a utilizar en este programa serán **introduction()**, la cuál se encargará de dar la bienvenida al usuario e introducir los numeros, y la otra función sera la cuál calcule las series, a la que llamaremos **series()**

```c
// Funciones globales

void introduction();
void serie();
```

## Función de introducción

Esta función se encarga de pedir el número de iteración por el que PI será calculado, tras esto, lo guardará en una variable creada en la sección de ["creación de las variables"](#Incluyendo-las-variables). Tras esto verificará si el número introducido es cero o negativo, si es el caso, pedira de nuevo un numero de iteraciónes e iniciará la [función de las series]()

```c

printf("Please enter the number of iterations you want to perform. \n");
scanf("%i", &iter);

    while(iter <= 0){
        printf("It seem you have entered a number that is less than or equal to 0, please enter a positive number. \n");
        scanf("%i", &iter);
    }
    serie();
```

En caso de que no lo supieras el carácter, '\n' permite que el siguiente mensaje apareza en la siguiente linea del terminal
{: .notice--info }

## Función de la serie

Lo siguiente se va a repetir hasta que la variable **cont** es mayor que el numero proporcionado para las iteraciones. A continuación se creará la variable **d** esta variable se encargará de la fracción realizada en la [formula](#breve-introducción) que hemos mostrado al principio, y creamos una variable que se denomine **result**, esta se encargará de añadir el resultado obtenido por la fracción (posteriormente lo múltiplicamos por 4 para obtener pi, ya que si no obtendriamos pi/4 y no pi)

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

En caso que no lo supieras, utilizamos el tipo 'dobule' en C por que tiene un limite de bytes que puede ser guardado en una sola variable, por lo que si hacemos iteraciones grandes, podría proporcionar errores no esperados.
{: .notice--info }

## Código final

El código final puede ser encontrado en [github](https://github.com/oviwanazul124/Leibniz-s-Algorithm-in-C/blob/main/main.c) page.
