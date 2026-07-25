---
title: Página para aprender Hiragana y Katakana
date: 2026-07-24 09:57:10 +0100
categories: [Coding, WebDev, Projects]
tags:
  - WebDev
  - Spanish
  - Projects

excerpt: Este es un post hablando sobre uno de los proyectos que he desarrollado se trata de una página para poder repasar o aprender Hiragana y Katakana en Japones

toc: true
toc_sticky: true
use_math: true

language: es
ref: japanese-learning-website
#lang_en: /en/japanese-learning-website
lang_es: /es/japanese-learning-website
#lang_ja: /jp/japanese-learning-website
permalink: /es/japanese-learning-website

header:
  overlay_image: /assets/images/japanese-learning-website/teaser-image.png
  overlay_filter: 0.25
  teaser: /assets/images/japanese-learning-website/teaser-image.png
---

# Objetivo

Este fue un proyecto que hice por necesidad ya que la página que solia usar para poder practicar hiragana y katakana desaparecio, así que replique una a mi estilo para poder utilizarla. Es bastante sencilla, pero me parecio un proyecto interesante.

## Código

El código es accesible en Github siendo que para la versión de Hiragana es [aquí](https://github.com/oviwanazul124/HiraganaPractice), mientras que para la versión de Katakana es [aquí](https://github.com/oviwanazul124/KanaPractice)

### HTML

Comenzando por el código HTML, se trata de un formulario conectado con un dos archivos de [JavaScript](#javascript). Primero observemos el código utilizado en el formulario.

```html
<div class="answerZone">
  <h2 id="kana">ア</h2>
  <p id="feedbackText"></p>
  <input type="text" id="inputKana" />
  <br />
  <button id="kanaSettingsTitle">Kana Settings (Click to Toggle)</button>
</div>

<!-- Continuación del código... -->
```

Como podemos observar tenemos un divisor que contenie, la zona de respuesta, donde tenemos un **H2** que es modificado via código de [JavaScript](#javascript) usando como placeholder la letra a de katakana, posteriormente un parrafo denominado como **feedbackText** que se encarga de mostrar al usuario si la lectura que ha introducido es correcta o no, y una zona de respuesta. Además encontramos una configuración donde podremos seleccionar que letras aparecerán o no.

Si miras el código proveniente de la versión de Hiragana podras ver que algunas IDs cambian pero la lógica detrás es la misma.
{: .notice--info}

En la foto de abajo podemos ver el resultado final.

![Photo-Answer](/assets/images/japanese-learning-website/teaser-image.png)

A continuación vamos a hablar de la sección HTML de la configuración de Katakana para ello la configuración esta conformado por grupos, agrupando las vocales principales, siendo que en este ejemplo nos centraremos en la vocal **A** para explicar el código

El código se repite igual en todos los grupos así que con explicar 1 es más que suficiente
{: .notice--info}

```html
<div id="kanaSettings" class="SettingsZone">
  <div id="kanaContent">
    <h5 id="kanaTitle">A</h5>
    <hr />
    <label><input type="checkbox" id="mARow" checked /> Select all </label>
    <br />
    <label><input type="checkbox" id="aRow" value="a" checked />ア</label>
    <!-- Continuación del código para las demás letras -->
  </div>
</div>
```

Cómo podemos observar tenemos un divisor principal para la configuración y otro para el contenido de katakana posteriormente cada valor de la vocal posee un h5 que muestra que valor de la vocal vamos a configurar. Además tenemos dos tipos de botones, uno de ellos que solo aparece una vez se trata del botón de seleccionar todo este botón se encarga de como su nombre indicar seleccionar que aparezcan todos los sonidos para poder ser estudiados, mientras que el otro botón que se repite tantas veces como botones existan es el botón del sonido individual, ambos guardan muchas similitudes solo que en el caso del botón de sonido individual también se incluye el valor de **value** esto posteriormente será relevante en la explicación del código de [JavaScript](#javascript)

![Photo-Settings](/assets/images/japanese-learning-website/settings.png)

### JavaScript

Primero de tdo tenemos dos archivos de JavaScript, el primer archivo que se llama **main.js** y el segundo archivo que se llama **globalcheckbox.js**, y comenzaremos con main.js

#### main.js

Main.js, como su nombre indica será el encargado principal de gestionar la generación al azar de las preguntas y verificar las respuestas. Lo primero que encontraremos es un diccionario, este diccionarío define la respuestas y vincula la letra elegida con su respuesta correcta como se puede ver en el ejemplo del código.

```javascript
const kana = [
  { kana: "ア", romanji: "a" },
  /* El código continua por cada letra*/
];
```

Despues de esto obtenemos el display para las preguntas, el input para poder leer la información del usuario, el parrafo para el texto de feedback y el botón de correción y por último una variable para controlar el item actual

```javascript
/* Código continua arriba */

const kanaDisplay = document.getElementById("kana");
const inputKana = document.getElementById("inputKana");
const feedbackText = document.getElementById("feedbackText");
const sumbitBtn = document.getElementById("sumbit");

let currentItem = null;

/* Código continua arriba */
```

Tras esto tenemos definidas ambas funciones [nextKana()](#nextkana) y [checkKana()](#checkkana). Y tras esto encontramos un código para modificar el comportamiento del botón que es el siguiente. Esto lo que hace es que cuando pulsemos enter en el navegador eliminará la acción por defecto y correra nuestra acción que sera la función [checkKana()](#checkkana)

```javascript
if (event.key === "Enter") {
  event.preventDefault();
  checkKana();
}
```

Por último tenemos el código para poder configurar los settings, para abrir y cerrarlo para ello obtenemos el titulo de los settings y el contenido de los settings, y añadimos un listener al evento de cuando es clickeado el titulo, haciendo que prevenga su comportamiento por defecto y que aplique la inversa de la visibilidad (Es decir si es visible que sea invisible y si es invisible que se visible).

```javascript
/* Código continua arriba */

const kanaSettingsTitle = document.getElementById("kanaSettingsTitle");
const kanaContentSettings = document.getElementById("kanaSettings");

kanaSettingsTitle.addEventListener("click", function () {
  event.preventDefault();
  kanaContentSettings.hidden = !kanaContentSettings.hidden;
});
```

##### nextKana()

Esta función es la encargada de generar la siguiente letra que va a aparecer en el la página para poder ser adivinada

```javascript
function nextKana() {
  const selectedKana = document.querySelectorAll(
    '#kanaSettings input[type="checkbox"]:checked',
  );

  const activeKanaValues = Array.from(selectedKana).map((box) => box.value);

  if (activeKanaValues.length == 0) {
    feedbackText.textContent = "Please select at least one";
    return;
  }

  /* El código continua aquí */
}
```

Como podemos observar la función comienza obteniendo aquellos valores que hemos seleccionado para estudiar y los guarda en la constante **selectedKana** y posteriormente los mapea según la constante para comprobar cuales de ellos estan activos. Si por un casual el usuario ha seleccionado 0 en el texto de feesdback se le mostrará **Please select at least one**.

```javascript
function nextKana() {
  /* El código que hemos visto arriba */

  const activeKana = kana.filter((item) =>
    activeKanaValues.includes(item.romanji),
  );

  const randomIndex = Math.floor(Math.random() * activeKana.length);

  currentItem = activeKana[randomIndex];

  kanaDisplay.textContent = currentItem.kana;

  inputKana.value = "";

  feedbackText.textContent = "";
}
```

A continuación lo que hace este código es obtener de los items que están activos su respuesta en romanji y guardarla, y generar el indice al azar que será usado para poder seleccionar la letra al azar para poder mostrar al usuario, guardandolo en la variable **currentItem** posteriormente mostrará en el contenido de la respuesta y reiniciará tanto la respuesta como el feedback.

#### checkKana()

Ahora vamos a analizar la siguiente función que es **checkKana()**, esta función lo primero que hace es comprobar si existe un item actual si no, devuelve vacio. Tras esto toma el valor del usuario sin mayusculas y lo guarda en la variable **kanaUser**, lo siguiente que hace es comprobar si la respuesta es correcta o no, proporcionando feedback al al usuario

```javascript
function checkKana() {
  if (!currentItem) return;

  const kanaUser = inputKana.value.toLowerCase();

  if (kanaUser == currentItem.romanji) {
    setTimeout(nextKana, 750);
    feedbackText.textContent = "Correct";
  } else {
    setTimeout(nextKana, 750);
    feedbackText.textContent =
      "Incorrect. The writing is " + currentItem.romanji;
  }
}
```

## Enlaces y github.

El proyecto puede ser visitado directamente desde sus páginas web siendo respectivamente [Katakana](https://oviwanazul124.github.io/KanaPractice/) y para [Hiragana](https://oviwanazul124.github.io/HiraganaPractice/)
