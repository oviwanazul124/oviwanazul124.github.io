---
title: Developing an RPG in Godot - Movement and adding sprites
date: 2024-12-8 12:00:10 +0100
categories: [Game Develop]
tags: [Godot, Game Develop, Tutorial, Maths]
description: This is a series of blog posts about how to develop a RPG game in godot. In this blog we are covering the movement and adding sprites.
math: true
image:
  path:
  alt: A knight moving
---

## Movement

One of the basic things in video games is movement, which are rare games that don't have any type of movement but exist. But now I am going to talk about movement in 2D games.

### Mathematics and Physics of the 2D Movement

First, we need to understand how movement works in 2D. Then, we could talk about a third dimension. But the third dimension will be shown in a future blog post. Movement in video games comes from a vector. Right now, I would not enter too deeply into the concept.

$$\vec{B}=\begin{bmatrix}
  \vec{i}, \vec{j}
\end{bmatrix}$$

![Vector-Base](assets/photos/Develop-an-RPG-2/Vector-Base.png)
_Example of the vector base_

>**i** is the same as if I say **x**, **j** is the same as if I say **y**.
{: .prompt-info}

Most of the movement comes when a vector changes, if we define a vector named for example **u** from movement.

$$\vec{u}=\begin{bmatrix}
  0, 0
\end{bmatrix}$$

This vector means that our character is in the position x = 0 and y = 0. But if for example, our character moves 2 times up, the vector will change.

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

The classic RPG uses the 8-movement, this type of movement enables the player to move in all directions they want, using **W**, **A**, **S**, **D**.

First of all, we are going to create a new folder at the root of our project, the folder will have the name "Scripts". Here we are going to save all the scripts to use in our game.

![Godot-Explorer-Created-Scripts]()
_Created Folder Scripts_

After creating the folder script we are going to press left click and create a script.

### Code

The code we are going to write is the following.

```gdscript
extends CharacterBody2D
```

Now we are going to understand this line of code, **extends CharacterBody2D**, extends is in charge of importing all the functions associated to [CharacterBody2D](https://docs.godotengine.org/en/stable/classes/class_characterbody2d.html)

> If you wanna know more about the CharacterBody2D click in his name and you will be redirected to the official documentation of Godot.
{: .prompt-info}

Now we have added two new lines of code, this is how you define variables in Godot you put **var [name of the variable] = [value]**, but what is the @export? When you see this type of word with an "@" is used to indicate to the engine something about the variable in this case to export it, this means that you will see this variable in the engine and be able to modify it from there without the necessity of going to the script.

#### Variables

```gdscript

extends CharacterBody2D

@export var walking_speed = 400
@export var running_speed = 800
```

#### Functions

Next, we are going to define de two main variables of this script the first one is **get_input()**, as his name shows this is where we are going to get the input from, and the other one is **_physics_process(delta)**, this is a function that comes with some nodes in godot, is in charge of updating the physics every frame.

> The variable delta is used when you update something every frame, is a really interesting variable and there will be a deeper in a future blog post.
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

#### Function get_input()

Now we are going to center in the function **get_input()**. This function is in charge to get the vector of direction of the input keys, **left**, **right**, **up**, **down**. But what are these input keys?. In a moment we are going to see it, for now we are going to talk about the if statement that we see here, this is in charge of seeing if the player want to run or to walk, if the key **shift** is pressed the code is going to use the **running_speed** but if it not being pressed is going to use the **walking_speed**

```gdscript
func get_input():
  var input_direction = Input.get_vector("left", "right", "up", "down")
  if Input.is_action_just_pressed("shift"):
    velocity = input_direction * running_speed
  else:
    velocity = input_direction * walking_speed
```

#### Setting up input commands

Opening the input controller map windows, we are going to set up the different input keys,

![Godot_Input_Map]()
_Godot Input Map Window_


#### Function _physics_process(delta)

```gdscript
  func _physics_process(delta):
    get_input()
    move_and_slide()
```
