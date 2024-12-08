---
title: Developing an RPG in Godot - Movement and adding sprites
date: 2024-12-8 12:00:10 +0100
categories: [Game Develop]
tags: [Godot, Game Develop, Tutorial, Maths]
description: This is a series of blog posts about how to develop a RPG game in godot. In this blog we are covering the movement and adding sprites.
math: true
image:
  path:
  alt: Godot Enginge Web Page
---

## Movement

One of the basic things in video games is movement, which are rare games that don't have any type of movement but exist. But now I am going to talk about movement in 2D games.

### Mathematics and Physics of the 2D Movement

First of all we need to understard how movement works in 2D, then we could talk about a third dimension. But the third dimension will be shown in a future blog post

First of all we need to understard that movement in videogames comes from a vector. Right I would no enter too deeply in the concept

$$\vec{B}=\begin{bmatrix}
  \vec{i}, \vec{j}
\end{bmatrix}$$

![Vector-Base](assets/photos/Develop-an-RPG-2/Vector-Base.png)
_Example of the vector base_

>**i** is the same as if I say **x**, **j** is the same as if I say **y**.
{: .prompt-info}

Most of the movement comes when a vector changes if we define a vector named for example **u** from movement.

$$\vec{u}=\begin{bmatrix}
  0, 0
\end{bmatrix}$$

This vector mean that our character is in the position x = 0 and y = 0. But if for example our character moves 2 times up, the vector will change.

$$\vec{u}=\begin{bmatrix}
  0, 2
\end{bmatrix}$$

![Vector-Example](assets/photos/Develop-an-RPG-2/Vector-Example.png)
_Example of the vector movement_

If you see the vector u is formed by two times the vector j

$$\vec{u}=\begin{bmatrix}
  2\vec{i}, 0
\end{bmatrix}$$

This is the basics you will need to know to understand movement in videogames. In the future there will be more in deep blog post.

## Movement in Godot

### Brief explanation

The classics RPG uses the 8-movement, this type of movement enables to the player to move in all directions they want, using **W**, **A**, **S**, **D**.

First of all we are going to create a new folder in the root of our project, the folder will have the name of "Scripts". Here we are going to save all the script to use in our game.

![Godot-Explorer-Created-Scripts]()
_Created Folder Scripts_

After creating the folder script we are going to press left click and create a script

### Code

The code we are going to write is the following the first of all we are going to use 

```gdscript
extends CharacterBody2D
```

Now we are going to understard this line of code, **extends CharacterBody2D**, extends is in charge of importing all the functions associated to [CharacterBody2D](https://docs.godotengine.org/en/stable/classes/class_characterbody2d.html)

> If you wanna know more about the CharacterBody2D click in his name and you will be redirected to the official documentation of Godot.
{: .prompt-info}

Now we have added two new lines of code, this is how you define variables in godot you put **var [name of the variable] = [value]**, but what is the @export?. When you see this type of words with an "@" is used to indicate to the engine something about the variable in this case to export it, this means that you will see this variable in the engine and be able to modify from there without the necessety of going to the script.

```gdscript

extends CharacterBody2D

@export var walking_speed = 400
@export var running_speed = 800
```

Next we are going to define de two main variables of this script the first one is **get_input()**, as his name shows this is where we are going to get the input from, the other one is **_physics_process(delta)**, this is a function that comes with some nodes in godot, is in charge of updating the physics every frame.

> The variable delta is used when you update something every frame, is a really interesting variable and there will be a more deep in a future blog post.
{: .prompt-info}

```gdscript

extends CharacterBody2D

@export var walking_speed = 400
@export var running_speed = 800

func get_input():
  pass

func _physics_process(delta):
  pass
```

Now we are going to center in the function **get_input()**.

