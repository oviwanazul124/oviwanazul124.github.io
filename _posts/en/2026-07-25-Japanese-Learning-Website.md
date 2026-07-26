---
title: Page to learn Hiragana and Katakana
date: 2026-07-24 09:57:10 +0100
categories: [Coding, WebDev, Projects]
tags:
  - WebDev
  - English
  - Projects

excerpt: This is a post talking about one of the proyects I developed, it is a page where you can learn or review Hiragana and Katakana in Japanese.

toc: true
toc_sticky: true
use_math: true

language: en
ref: japanese-learning-website
lang_en: /en/japanese-learning-website
lang_es: /es/japanese-learning-website
lang_ja: /jp/japanese-learning-website
permalink: /en/japanese-learning-website

header:
  overlay_image: /assets/images/japanese-learning-website/teaser-image.png
  overlay_filter: 0.25
  teaser: /assets/images/japanese-learning-website/teaser-image.png
---

# Objective

This is a project I made as the page I used to review Hiragana and Katakana was closed down or removed by the author, so I replicated the feeling and the use to be able to review again. It is really simple, but is a really interesting project

## Code

The code can be viewed in Github for the Hiragana version is [here](https://github.com/oviwanazul124/HiraganaPractice), while for the Katakana version can be see [here](https://github.com/oviwanazul124/KanaPractice)

### HTML

Starting with the HTML code, it is a simple form connected to two JavaScript files [JavaScript](#javascript). First we are going to see the code used in the form.

```html
<div class="answerZone">
  <h2 id="kana">ア</h2>
  <p id="feedbackText"></p>
  <input type="text" id="inputKana" />
  <br />
  <button id="kanaSettingsTitle">Kana Settings (Click to Toggle)</button>
</div>

<!-- The code continue here...-->
```

As we can see we have a div that contains the answer zone, where we have a **h2** that is modified via code of the [JavaScript](#javascript) file using as a placeholder the letter a of katakana, then there is a p named as **feedbackText**, his main function is to show to the user if the reading he has inputed is correct or not, and the last thing is the answer zone and the configs where we can select what letters we want to review or learn.

If you check the code coming from the Hiragana version you would see that some IDs changes but the logic is the same as the Katakana one.
{: .notice--info}

In the photo you can see the final version with CSS.

![Photo-Answer](/assets/images/japanese-learning-website/teaser-image.png)

Now we are going to talk about the HTMl section of the Katakana configuration for this we can see is divided in groups, the groups is formed by the vocals, in the example code we will se is going to be for the **A** vocal.

The code is the same for all the vocals so only one is necessary to be explained.
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

As we can see we have a main div for the config and a nother one for the content of the Katakana after this every value of the vocal have an H5 that shows the value of the vocal we are going to configure. We also have to type of buttons, one of them only appear one time and is the button to select all of the vocals to be studied, while the other button is repeat the times of the different variants of that vocal, both of them has almost all the same values except the one with every value has the atribbute value that is passed for the files of [JavaScript](#javascript).

![Photo-Settings](/assets/images/japanese-learning-website/settings.png)

### JavaScript

First of all we have two main JavaScript files, the first one is named **main.js** and the second one is called **globalcheckbox.js**. We are going to start with the main.js file.

#### main.js

Main.js, as his name shows is going to be the files in charge of all the logic of the website, the randomness of the letters and checking the answers, first of all, we are going to see a dictionary where every letter of Katakana is assigned a correct answer, as it can be seen in the example below.

```javascript
const kana = [
  { kana: "ア", romanji: "a" },
  /* The code continues below...
];
```

After this we have a number of variables were we assign the inpout to read the info of the user, the p that we have mentioned before, the feedback to show if it is correct or incorrect and more variables.

```javascript
/* The code continues up... */

const kanaDisplay = document.getElementById("kana");
const inputKana = document.getElementById("inputKana");
const feedbackText = document.getElementById("feedbackText");
const sumbitBtn = document.getElementById("sumbit");

let currentItem = null;

/* The code continues below */
```

After this we have defined to functions the first one is [nextKana](#nextkana) and the second one is [checkKana](#checkkana) below both definitions of the functions we can see a javascript code to modify the function of the enter key, to be able to the user to answer the questions without applying the default value of the key.

```javascript
if (event.key === "Enter") {
  event.preventDefault();
  checkKana();
}
```

The las part of the code is the settings logic, this code is in charge to be able to open and close the settings to make it easier for the user to concentrate, we have the listener that checks if the buttons has been clicked, if it is the case it prevents his normal behaviour and then apply the inverse of the visibility.

```javascript
/* The code continue up */

const kanaSettingsTitle = document.getElementById("kanaSettingsTitle");
const kanaContentSettings = document.getElementById("kanaSettings");

kanaSettingsTitle.addEventListener("click", function () {
  event.preventDefault();
  kanaContentSettings.hidden = !kanaContentSettings.hidden;
});
```

##### nextKana()

This function is in charge to generate the next letter that is going to appear in the web page.

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

  /* The code continues here... */
}
```

As we can see the function starts obtaining the values of the letters we have selected to study and save it in the variable name **selectkedKana** after that it maps it with his correct answer to know what are the ones active and not. If the user dosen't select any letter to be studied the feedback text will be changed to **Please select at least one**

```javascript
function nextKana() {
  /* The code we have seen up */

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

Next the code obtains the letters that are active and writes and checks it with his romanji answer, and generate a random index to be select the letter to show to the user, and saves it to the **currentItem** variable, that will be show in the content of the answer and at last reset the value of the answer and the feedback text.

#### checkKana()

Now we are going to check the next funciont that is **checkKana()** this function is in charge of checking if it exist a real actual item of not, if is empty it returns null. If it exist a value set it to lower case and save it to the variable **kanaUser** then checks if the answer is correct o is not correct giving feedback to the user.

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

## Links and github

The proyect can be checked via his respective pages on github being the [Katakana](https://oviwanazul124.github.io/KanaPractice/) and this for the [Hiragana](https://oviwanazul124.github.io/HiraganaPractice/)
