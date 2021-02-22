# Core Online Music Stuff

This contains all my progress to date and serves as a reference for me when making online interactive music and art projects. At the time of writing this project contains what I've learned about the following:

* HTML
* CSS
* JavaScript
* p5.js for graphics and animation (I have stopped using their sound library or their event listeners)
* Tone.js
* Netlify
* Github

# HTML

Not using much of this in here, however the orchlab french horn uses more of it. Using the event listeners directly on divs in that way is quite nice, however I did find it all a bit clunky and uninspiring for designing things.

Adding `<span class="clear"></span>` keeps the menus formatted correctly.

Putting the Javasccript within a div is a good idea. It allows for a lot more flexibility particularly with using p5.js with vamilla JavaScript for a better touch and mouse experience (and code that can easily port to another graphics libray).

The JavaScript script needs to be referenced within the body if you want to be able to interact between HTML and JS.

# CSS

A really big one is that to dynamically change the size of a p5.js sketch, the best way I have learned so far is to do it in CSS. When I change it in JS it doesn't always match the other DOM elements in unpredictable ways.

Dynamically change the p5 canvas to always fill the parent div width.  The width of the canvas from p5 is dynamically created, meaning that it gets applied at element level. There is no way of overriding that with specificity, so you need to raise a declaration as `!important:`.

    #mycanvas {
    float: left;
    width: 100% !important;
    height: 100% !important;
    }

Then you have to place the canvas within a parent div which has the correct attributes to dynamically create the right dimensions.

    #p5parent {
    float: left;
    height: 100%;
    width: 100%;
    }

I'm also using the CSS to do media queries and change display depending on screen size and orientation.

    @media (min-aspect-ratio: 3/2) {
    .containerclass{
        position: relative;
        width: 48%;
        display: block;
        margin-left: auto;
        margin-right: auto;
    }
    }

    @media (min-aspect-ratio: 16/17) and (max-aspect-ratio: 3/2) {
    .containerclass{
        width: 60%;
        display: block;
        margin-left: auto;
        margin-right: auto;
    }
    }

    @media (max-aspect-ratio: 16/17) {
    .containerclass{
        width: 100%; /* set to 102% to hack around an issue with space to the right in portrait mode*/
        display: block;
        margin-left: auto;
        margin-right: auto;
        }
    }

For the select boxes there is a lot of CSS which comes from a tutorial on [w3schools.com](https://www.w3schools.com/howto/howto_custom_select.asp).

# JavaScript

I haven't used it in this project, but you can declare a whole stack of variables at once with let in one statement. I'm still getting my head around let, var etc. so more soon! For example I just read that var can create a property on a global object, while let can't. Will need to investigate this further.

You can add event listeners to the entire document or to individual items in the DOM.

    let masterDiv = document.getElementById("container");
    let divPos = masterDiv.getBoundingClientRect();

`element.getBoundingClientRect();`The returned value is a DOMRect object which is the smallest rectangle which contains the entire element, including its padding and border-width. The left, top, right, bottom, x, y, width, and height properties describe the position and size of the overall rectangle in pixels.

`let masterLeft = divPos.left;` distance from left of screen to left edge of bounding box.

`let masterRight = divPos.right;` distance from left of screen to the right edge of bounding box.

`let cnvDimension = masterRight - masterLeft;` size of div - however in some cases this is wrong, so i am now using CSS !important to set the size and scaling, which also behaves more as I imagined - but have kept this to work out size of other elements if needed.

`cnv.id('mycanvas');`  assign id to the canvas so i can style it - this is where the css dynamic sizing is applied.

`cnv.parent('p5parent');` put the canvas in a div with an id if needed so it can be placed on the screen using HTML - this DIV also needs to be sized correctly, and when you change this one, the one within will change to match it.

`let el = document.getElementById("p5parent");`

`el.addEventListener("touchstart", handleStart, false);` I also assign the vanilla JS event listeners to the DIV containing the canvas.

`offset = el.getBoundingClientRect();`  get the size and position of the p5parent div so i can use offset.top to work out where touch and mouse actually need to be allowing for the othe elements in the DOM.

    for (let i = 0; i < numberOfButtons; i++) {
    mouseState.push(0);
    }

I've started trying to code in a more dynamic way - so that changing a single variable changes many things. Sometimes I need to use an array to store the state of things, and this is an example of how to fill this with default values in this case.

# P5.js

AT the time of writing I am only using p5 for drawing and potentially for animation.

Giving the canvas an id and placing it in a parent DIV is important so it can be targetted for CSS styling, positioning in the DOM and event listeners etc being added to it.

I have stopped using the sound library as I found it to be slow and unreliable.

I have stopped using the p5 touch functions as they are incomplete, so I'm using vanilla JS ones instead.

As a consequence of not using the p5 touch, I have also stopped using the p5 mouse functions too, otherwise touch and mouse interfere with each other.

`colorMode(HSB, 5);` HSB colour is new to me, but I think I like it! It appears to be much easier to understand as it maps the colours around a circle. So the first value is hue, the second saturation, and the third brightness. In this case by assigning the second parameter to the number 5, the entire range is reduced to five, and divided by five. So instead of having a number between 0 and 360 to pick a hue, I have a number between 0 and 5. In this case if I was to use the number 3 it would be the equivelent of (360/5) * 3. This allows for a simple automation of colours split equally around the colour wheel. I've assigned this parameter to a variable in my code.
