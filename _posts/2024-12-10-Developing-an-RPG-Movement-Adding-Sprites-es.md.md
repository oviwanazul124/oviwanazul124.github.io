---
layout: default
title: "Desarrollando un RPG: Movimiento y añadiendo sprites"
lang: es
categories: [en, GameDev]
tags: [GDScript, Godot, RPG]
lang_ref: RPGMov
---

## Movimiento

Una de las cosas más básicas en videojuegos es en movimiento, son raro los juegos que no tienen algún tiempo de movimiento, aunque existen. Pero por ahora vamos a centrarnos en movimiento en juegos 2D.

### Matemática y física del movimiento 2Dement

Primero debemos compreder como funciona el movimiento en 2D, para entonces poder hablar de una tercera dimensión. Desarrollaremos el tema del movimiento 3D en un post futuro del blog. De forma resumida el movimiento en videojuegos proviene de un vector.

$$
\vec{B}=\begin{bmatrix}
  \vec{i}, \vec{j}
\end{bmatrix}
$$

![Vector-Base](assets/photos/Develop-an-RPG-2/Vector-Base.png)
_Ejemplo del vector base_

> **i** es lo mismo que si dijera **x** y **j**, es lo mismo que si dijera **y**.
> {: .prompt-info}

El movimiento proviene de cuando un vector, se ve alterado. Por ejemplo si definimos un vector **u** para el movimiento.

$$
\vec{u}=\begin{bmatrix}
  0, 0
\end{bmatrix}
$$

Este vector nos muestra que nuestro personaje se encuentra en la posición x = 0 y en y = 0. Pero si por ejemplo, movieramos nuestro personaje 2 veces hacía arriba este vector cambiaría.

$$
\vec{u}=\begin{bmatrix}
  0, 2
\end{bmatrix}
$$

![Vector-Example](assets/photos/Develop-an-RPG-2/Vector-Example.png)
_Ejemplo de un vector de movimiento_

Si observar el vector u esta formado por dos veces el vectro j

$$
\vec{u}=\begin{bmatrix}
  2\vec{i}, 0
\end{bmatrix}
$$

Esto es lo más básico para poder entender un movimiento muy básico en videojuegos. En el futuro desarrollaremos mucho más

## Movimiento en Godot

### Breve explicación

El RPG clasico utiliza un movimiento en 8 direcciones, este tipo de movimiento permite al jugador moverse en dichas 8 direcciones, utilizando **W**, **A**, **S**, **D**.

Lo primeor de todo, tendremos que crear una nueva carpeta en la raíz de nuestro proyecto, con el nombre de "Scripts". Aquí guardaremos todos los scripts que usaremos en nuestro juego.

![Godot-Explorer-Created-Scripts](assets/photos/Develop-an-RPG-2/Created-Folder-Scripts.png)
_Carpeta Scripts Creada_

Despues de crear la carpeta "Scripts", vamos a pulsar click izquierdo y crear un nuevo script.

### Código

El código que vamos a escribir es el siguiente:

```gdscript
extends CharacterBody2D
```

Ahora vamos a entender esta line de código, **\*extends CharacterBody2D**, 'extends' es el encargado de importar todas las funciones asociadas al [CharacterBody2D](https://docs.godotengine.org/en/stable/classes/class_characterbody2d.html)

> Si quieres saber más acerca del CharacterBody2D haz click en su nombre y te redireccionará a la documentación oficial de Godot.
> {: .prompt-info}

#### Variables

```gdscript

extends CharacterBody2D

@export var walking_speed = 400
@export var running_speed = 800
```

Ahora vamos a añadir dos nuevas lineas de código, si no lo recordamos una variable se define a través de **var [nombre de la variable] = [valor]**, ¿Pero que significa el @export de a lado?. Cuando ves una palabra a lado de una "@" se usa para indicar que debe realizar algo con la variable, en este caso exportarla al editor. Esto significa que cuando volvamos al editor veremos la variable en él.

#### Funciones

Lo siguiente que vamos a hacer es definir las dos funciones principales de este script, la primera es **get_input()**, como su nombre indica será la función que nos otorgue el input del jugador y la otra función es **\_physics_process(delta)**, esta es una función que viene con algunos nodos de godot, y se encarga de llamar al código que se encuentra dentro cada frame.

> La variable delta es una variable muy importante en el desarrollo de videojuegos, y realizaremos un blog desarrollandola más en el futuro.
> {: .prompt-info}

```gdscript

extends CharacterBody2D

@export var walking_speed = 400
@export var running_speed = 800

func get_input():
  pass

func _physics_process(delta):
  pass
```

### Función get_input()

Ahora vamos a centrarnos en la función **get_input()**. Esta función se encarga de obtener el vector de dirección que obtienen las teclas de input, **izquierda**, **dereche**, **arriba**, **abajo**. ¿Pero que son estas teclas de input?, lo veremos en un momentos, por ahora vamos a hablar además del if que nos encontramos ahí, este se encarga de verificar si el jugador quiere correr o andar, si pulsa la tecla **shift** el código usará la variable **running_speed** pero si no esta siendo presionada usará **walking_speed**.

```gdscript
func get_input():
  var input_direction = Input.get_vector("left", "right", "up", "down")
  if Input.is_action_just_pressed("shift"):
    velocity = input_direction * running_speed
  else:
    velocity = input_direction * walking_speed
```

#### Configurando los comandos de input

Para abrir el mapa de input debemos seguir los siguientes pasos, primero tendremos que irnos a **proyecto**, luego a **configuración de proyecto** y por último **Input Map**

![Godot_Input_Map](assets/photos/Develop-an-RPG-2/Godot-Input-Map-Window.png)
_Ventada de Mapa de Input Godot_

Despues de esto vamos a escribir donde pone **"Añadir una nueva acción"**, y escribiremos **left**, despues pulsaremos **Añadir**, cuando lo pulsemos veremos los siguientes cambios.

![Godot_Input_Map_Added_Input](assets/photos/Develop-an-RPG-2/Godot-Iput-Map-Added-Input.png)
_Mapa de Input añadido en Godot_

Lo siguiente que vamos a hacer es pulsar el **signo de más**, y presionar la tecla que queremos añadir a ese input. Despues pulsaremos **aceptar**.

![Godot_Input_Map_Added_Input_Key](assets/photos/Develop-an-RPG-2/Godot-Input-Map-Added-Input-Key.png)
_Godot Input Map Added Input Key_

Ahora debemos hacer el mismo proceso para las teclas **right**, **up** y **down**.

#### Función \_physics_process(delta)

Ahora vamos a explicar la función **\_physics_process(delta)** esta función es creada por el propio motor y se encarga de lo relacionado con las físicas, desde aquí llamaremos a la función anterior **get_input()**, y a la función **move_and_slide**, esta función también esta creada por el motor, y dice cuando el objeto tiene que moverse.

```gdscript
  func _physics_process(delta):
    get_input()
    move_and_slide()
```

> Si recibes un aviso en **delta** añade un guión así "**\_delta**"
> {: .prompt-warning}

## Añadiendo el script y creando el jugador

Lo siguiente que vamos a hacer es pulsar click izquierdo en el **Node2D** y presionar **Añadir Hijo**, se abrirá una ventana en la que tenemos que buscar **CharacterBody2D** y añadirlo.

![Adding_CharacterBody2D](assets/photos/Develop-an-RPG-2/Adding-CharacterBody2D.gif.gif)
_Añadiendo un CharacterBody2D_

> Si no tienes un **Node2D** ahí, añadelo de la misma forma que has añadido el characterBody2D.
> {: .prompt-warning}

Vas a ver un pequeño icono de aviso a lado de su nombre, por ahora no debes darle importancia. Despues de eso, haz lo mismo pero esta vez haciendo click en **CharacterBody2D**, y añadiendo un **Sprite**.

![Adding_Sprite](assets/photos/Develop-an-RPG-2/Adding-Sprite.gif)
_Añadiendo un Sprite_

Ahora solo hay una cosa más que hacer y es añadir el script al CharacterBody2D.

![Adding_Script_To_CharacterBody2D](assets/photos/Develop-an-RPG-2/Adding-Script-To-CharaterBody2D.gif)
_Añadiendo el script al CharacterBody2D_

## Github Demo

Aquí puedes acceder al [repo](https://github.com/oviwanazul124/How-to-make-an-RPG/tree/main/Developing%20an%20RPG%20in%20Godot%20-%20Movement%20and%20adding%20sprites) que contiene los diferentes archivos de como hemos desarollado el RPG.
