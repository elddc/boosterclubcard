# Fremd Booster Club Digital Cards

This project digitizes Fremd Booster Club's membership cards to improve access while reducing mailing and printing costs.

The viking head logo is taken from the [Fremd Booster Club website](https://www.fremdboosterclub.org/sites/all/themes/educational1/logo.png).

## Documentation

This project is made in vanilla JS/HTML/CSS. There is a separate `.html` file for each type of card, 
with a single stylesheet shared across all pages.

Below is a thorough beginner-friendly explanation, to allow for easy modification

### File Directory

* `styles.css` &larr; styles live here
* `assets/ `
  * `logo.png`     &larr; logo on card, icon (image in browser tab)
* `pages/`
  * `...` &larr; html files for each card, see below for template with comments

### HTML Template

See comments for an explanation of what each section is
```html
<!-- This is a comment -->

<script>
  //This is a comment inside a script tag
</script>
```
The roles of each line are described by the class name, for example the year:
```html
<div class="year" />
```

Text in ALL CAPS is editable text to display on the card

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

    <!-- styling -->
    <link rel="stylesheet" href="styles.css">
</head>
<body>
<div class="container">
    <div class="card">
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
                <br/>
                DESCRIPTION - SECOND LINE (OPTIONAL)
            </div>
            <div class="signature">
                <label for="input">Buyer Name:</label>
                <input type="text" id="input" placeholder="Type Name Here"/>
            </div>
        </div>
        
    </div>
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

</script>
</body>
</html>
```

To create a line break, use this symbol: 
```html
<br/>
```