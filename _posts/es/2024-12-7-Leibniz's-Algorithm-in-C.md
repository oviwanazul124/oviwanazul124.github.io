---
title: Algoritmo de Leibniz en C
date: 2024-12-7 17:42:10 +0100
categories: [Programming]
tags: [c, Tutorial, Español]
description: Short tutorial on how to develop Leibniz's algorithm in C.
math: true
lang: es
permalink: /es/leibnizs-algorithm-in-c/
translations:
  ja: /ja/leibnizs-algorithm-in-c/
  en: /posts/Leibniz's-Algorithm-in-C/
  es: /es/leibnizs-algorithm-in-c

---

## Breve introducción

Para desarrollar el algoritmo de Leibniz en C primero debemos conocer de donde proviene el algoritmo. Aquí está la formula matemática del algoritmo o serie:

$$\sum_{n=0}^\infty\frac{(-1)^n}{2n + 1} = \frac{\pi}{4}$$

## Proceso de desarrollo

### Librerias incluidas

Primero necesitamos importar las siguientes librerias.

```c
#include <stdio.h>
#include <math.h>
```

> ¡Asegurate de importarlas o tendrás errores en el futuro!
{: .prompt-danger }

La libreria "stdio" es la libreria estándar de C, mientras que "math.h" es la libreria que usaremos para encargarnos de las matemáticas más complejas (Si decides usar la formula de arriba, no necesita importarla)

### Incluyendo todas las las variables

La siguiente cosa que tendremos que hacer sera crear las variables las cuáles serán "**iter**", esta variable se encargara de mostrar las diferenes iteraciones que hemmos realizado, luego la variable "**cont**" que cuenta el numero de iteraciones que originalmente a introducido el usuario. Por último añadiremos la variable "**pi**", que incluirá una serie de digitos de pi para poder calcular el error en la serie.

```c
int iter;
int cont = 0;
float pi = 3.141592653589793;
```

### Las funciones

Usaremos dos functiones en este programa, la primera función será "**introduction()**", se encargará de dar la bienvenida al usurio y pedirle introducir los números, la otra función será la que calcule la serie y se llamará "**series()**"

```c
// Funciones globales

void introduction();
void serie();
```

## Función de la función introducción

Esta funcion se encarga de pedir al usuario el numero de iteraciones por las que pi debe ser cálculado, despues lo guarda en una variable que hemos creado en [incluyendo todas las variables](#incluyendo-todas-las-las-variables). Después de esto verifica si el número es 0 o negativo, ya que si este es el caso pedirá al usuario reintroducir otro nnúmeo y finalmene llama a la [función series]()


```c

printf("Por favor introduzca el número de iteraciones que desea realizar. \n");
scanf("%i", &iter);

    while(iter <= 0){
        printf("Parece que el número de iteraciones que has introducido es un número negativo o 0. \n");
        scanf("%i", &iter);
    }
    serie();
```


> Si no lo sabías, ‘\n’ permite que el siguiente mensaje aparezca en una nueva linea.
{: .prompt-info }


## Función de la función serie

A continuación usaremos un while que comprobará si la variable **cont** es mayor que el número que ha introducido el usuario. Lo sigueinte que hará será crear la variable **d**, que se encargará de la división de la [fórmula](#breve-introducción) que hemos enseñado al principio, después definimos otra variable llammada **result**, esto nos permitira añadir el resultado de la fracción obtenida (Lo múltiplicamos por 4 por que si nos daría pi/4 no pi)
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

El código final puedes encontrarlo en mi página de [github](https://github.com/oviwanazul124/Leibniz-s-Algorithm-in-C/blob/main/main.c).
