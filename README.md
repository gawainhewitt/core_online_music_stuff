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

Adding `<span class="clear"></span> keeps the menus formatted correctly.`

Putting the Javasccript within a div is a good idea. It allows for a lot more flexibility particularly with using p5.js with vamilla JavaScript for a better touch and mouse experience (and code that can easily port to another graphics libray).

The JavaScript script needs to be referenced within the body if you want to be able to interact between HTML and JS,

# CSS

A really big one is that to dynamically change the size of a p5.js sketch, the best way I have learned so far is to do it in CSS. When I change it in JS it doesn't always match the other DOM elements in unpredictable ways.

    #mycanvas {  /* dynamically change the p5 canvas to always fill the parent div width.  The width of the canvas from p5 is dynamically created, meaning that it gets applied at element level. There is no way of overriding that with specificity, so you need to raise a declaration as !important: */
    float: left;
    width: 100% !important;
    height: 100% !important;
    }

    #p5parent { /* then you have to place the canvas within a parent div which has the correct attributes to dynamically create the right dimensions */
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
        /* border: 5px solid red; */
    }
    }

    @media (min-aspect-ratio: 16/17) and (max-aspect-ratio: 3/2) {
    .containerclass{
        width: 60%;
        display: block;
        margin-left: auto;
        margin-right: auto;
        /* border: 5px solid blue; */
    }
    }

    @media (max-aspect-ratio: 16/17) {
    .containerclass{
        width: 100%; /* set to 102% to hack around an issue with space to the right in portrait mode*/
        display: block;
        margin-left: auto;
        margin-right: auto;
        /* border: 5px solid yellow; */
        }
    }
