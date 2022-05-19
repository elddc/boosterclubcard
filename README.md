# Fremd Booster Club Digital Cards

This project digitizes Fremd Booster Club's membership cards to improve access while reducing mailing and printing costs.

The viking head logo is taken from the [Fremd Booster Club website](https://www.fremdboosterclub.org/sites/all/themes/educational1/logo.png).

## Documentation

This project is made in vanilla JS/HTML/CSS.
There is a separate `.html` file for each type of card, 
with a single stylesheet shared across all pages. 
It also uses the `dom-to-image` and `file-saver` libraries.

This page includes a thorough beginner-friendly explanation, to allow for easy modification.
If you are familiar with HTML/CSS/JS, you can disregard the rest of this document.

### Table of Contents
- [File Directory](#file-directory)
- [Explanations](#explanations)
- [Page Template](#full-html-template)

### File Directory

* `styles.css` &larr; styles live here
* `assets/ `
  * `logo.png`     &larr; logo on card, icon (image in browser tab)
* `pages/`
  * `...` &larr; html files for each card, see below for template with comments

### Explanations

See comments for a description of what each section is:
```html
<!-- This is a comment -->

<script>
  //This is a comment inside a script tag
</script>

<style>
  /* this is a comment inside a .css document */
</style>
```
The roles of each line are described by the class name, for example the year:
```html
<div class="year" />2021-2022</div>
```

Text in `ALL CAPS` is editable text to control the content of the card.<br>
Be sure to replace all the text in `ALL CAPS`, including the color of the card:
```html
<!-- color can be a hex code: #RRGGBB 
                      or rbg: rbg(R,G,B) -->
<div class="card" style="background-color: COLOR;">...</div>
```
Line breaks can be added with this symbol:
```html
<br>
```

Note that some symbols (such as &) should be escaped, requiring a special code:
```html
'&#38' with a semicolon (;) produces '&#38;'
```

### Full HTML Template
Copy and paste this into a `.html` file to create a new page. 
Replace the text in `ALL CAPS`.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <!-- setting up page -->
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, height=device-height, initial-scale=1.0">
    
    <!-- text and image displayed in browser tab -->
    <title>Viking Booster Card</title>
    <link rel="icon" href="assets/logo.png" />

    <!-- Google Material Icons (for download button) -->
    <link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
    
    <!-- page styling (must go after Google styling) -->
    <link rel="stylesheet" href="styles.css">

    <!-- external libraries used to save image -->
    <script src="https://cdn.bootcss.com/FileSaver.js/2014-11-29/FileSaver.min.js"></script>
    <script src="https://cdn.bootcss.com/dom-to-image/2.6.0/dom-to-image.min.js"></script>
</head>
<body>
<div class="container">
    <div class="card" style="background-color: COLOR;">
        <!-- top part of card -->
        <div class="row">
            <img src="assets/logo.png" alt="Viking Logo"/>
            <div class="header">Fremd Viking Booster Club</div>
        </div>

        <!-- main content of card -->
        <div class="center">
            <div class="year">YYYY-YYYY</div>
            <div class="card-title">TYPE OF CARD</div>
            <div>
                DESCRIPTION - FIRST LINE
                <br>
                DESCRIPTION - SECOND LINE (OPTIONAL)
            </div>
            <div class="name">
                <label for="input">Buyer Name:</label>
                <input type="text" id="input" placeholder="Type Name Here"/>
            </div>
        </div>
    </div>

    <!-- download image button at lower right -->
    <button onClick="download()" class="download">
        <!-- this uses Google Material Icons, can also be replaced with an image -->
        <span class="material-icons">download</span>
    </button>
</div>

<!-- JavaScript code -->
<script>
  //remove focus on text input when Enter key is pressed
    document.querySelector('#input').addEventListener('keydown', ({key}) => {
      if (key === 'Enter')
        document.activeElement.blur();
    })
  
    //make card fit correctly on phones in landscape mode
    //if this is not important, the next few lines can be removed
    function resize() {
        //create/update CSS variable --vh based on visible area of screen
        document.documentElement.style.setProperty('--vh', `${window.innerHeight * 0.01}px`);
    }
    resize();
    //trigger resize() function when screen dimensions change
    window.addEventListener('resize', resize);
    
    //download image to device
    function download() {
        //convert HTML element with class 'card' to image
        //then save as 'boostercard.png'
        domtoimage.toBlob(document.querySelector('.card')).then((blob) => {
            window.saveAs(blob, 'boostercard.png'); //file name can be changed
        });
    }
</script>
</body>
</html>
```