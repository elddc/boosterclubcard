# Fremd Booster Club Digital Cards

This project digitizes Fremd Booster Club's membership cards to improve access while reducing mailing and printing costs.

The viking head logo is taken from the [Fremd Booster Club website](https://www.fremdboosterclub.org/sites/all/themes/educational1/logo.png).

## Documentation

This codebase is written for maximum readibility and maintainability, even for non-developers.

The project is made in vanilla JS/HTML/CSS.
There is a separate `.html` file for each type of card, 
with a single stylesheet shared across all pages. 
It also uses the `dom-to-image` and `file-saver` libraries.

This page includes a thorough beginner-friendly explanation, to allow for easy modification.
If you are familiar with HTML/CSS/JS, you can disregard the rest of this document.

### Table of Contents
- [File Directory](#file-directory)
- [Page Template](#full-html-template)
- [Explanations](#explanations)

### File Directory

* `styles.css` &larr; styles live here
* `logo.png` &larr; logo on card, image in browser tab
* `NAMEYYYY.html` &larr; html files for each card, see below for template with comments

### Full HTML Template
Copy and paste this into a `.html` file to create a new page. 
Replace the text in `[ALL CAPS]` with square brackets around them.

[Jump To Explanation](#explanations)

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- setting up page -->
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, height=device-height, initial-scale=1.0">
    
    <!-- text and image displayed in browser tab -->
    <title>Viking Booster Card</title>
    <link rel="icon" href="logo.png">

    <!-- set the background color of the card -->
    <style>
        :root {
            --background-color: [COLOR];
        }
    </style>
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    
    <!-- page styling (must go after Google styling) -->
    <link rel="stylesheet" href="styles.css">
    
    <!-- external libraries used to save image -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/FileSaver.js/2.0.5/FileSaver.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/dom-to-image/2.6.0/dom-to-image.min.js"></script>
</head>
<body>
<div class="container">
    <div class="card">
        <!-- top part of card -->
        <div class="row">
            <img src="logo.png" alt="Viking Logo"/>
            <div class="header">Fremd Viking Booster Club</div>
        </div>
        
        <!-- separator -->
        <div class="border"></div>

        <!-- main content of card -->
        <div class="center">
            <div class="year">[YYYY-YYYY]</div>
            <div class="card-title">[TYPE OF CARD]</div>
            <div>
                [DESCRIPTION - FIRST LINE]
                <br>
                [DESCRIPTION - SECOND LINE (OPTIONAL)]
            </div>
            <div class="name">
                <label for="input">Buyer Name:</label>
                <input type="text" id="input" placeholder="Type Name Here"/>
            </div>
        </div>
    </div>

    <!-- download image button at lower right -->
    <button onClick="download()" class="download">
        <!-- Google Material Icon, can also be replaced with an image -->
        <span class="material-icons">download</span>
    </button>
</div>

<!-- JavaScript code -->
<script>
    // make card fit correctly on phones in landscape mode
    // if this is not important, the next few lines can be removed
    function resize() {
        // create/update CSS variable --vh based on visible area of screen
        document.documentElement.style.setProperty('--vh', `${window.innerHeight * 0.01}px`);
    }
    resize();
    // trigger resize() function when screen dimensions change
    window.addEventListener('resize', resize);
    
    // remove focus on text input when Enter key is pressed
    document.querySelector('#input').addEventListener('keydown', ({key}) => {
        if (key === 'Enter')
            document.activeElement.blur();
    })
    
    // download image to device
    function download() {
        // set desired height of final image
        const imgHeight = 1000;
        
        // setup
        resize();        
        const card = document.querySelector('.card');
        const scale = imgHeight/card.offsetHeight;
        
        // convert HTML element with class 'card' to image, then save as 'boostercard.png'
        domtoimage.toPng(card, {height: imgHeight, width: card.offsetWidth * scale, style: {
                transform: `scale(${scale})`,
                transformOrigin: 'top left',
            }}).then((img) => {
            window.saveAs(img, 'boostercard.png');
        });
    }
</script>
</body>
</html>

```

### Explanations

See comments for a description of what each section is:
```html
<!-- This is a comment -->

<script>
  // This is a comment inside a script tag
</script>

<style>
  /* this is a comment inside a .css document */
</style>
```
The roles of each line are described by the class name, for example the year:
```html
<div class="year"/>2021-2022</div>
```

In the template, text in `ALL CAPS` is editable text to control the content of the card.<br>
Be sure to replace all the text in `ALL CAPS`, including the color of the card:
```html
<!-- color can be a hex code: #RRGGBB 
                      or rbg: rbg(R,G,B) -->
<style>
    :root {
        --background-color: [COLOR];
    }
</style>
```
Line breaks can be added with this symbol:
```html
<br>
```

Note that some symbols (such as &) should be escaped, requiring a special code:
```
&#38; produces &
```
