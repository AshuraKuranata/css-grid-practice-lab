# css-grid-practice-lab

## Introduction
This lab is oriented to synthesize the material around CSS Grid and all the application of the CSS lessons up to this point and try to create as many mock-ups of the <a href="https://www.figma.com/file/z6zxp0qSF0cRX9fBb5IEYT/Wireframing-(Copy)?type=design&node-id=0-1&mode=design&t=myZRZP2OmzqF7a2u-0">Figma files</a> presented here.

I will be attempting to create as many within a reasonable amount of practice, and will section off this readme as each page is complete.

In preparation for this, I will also be creating HTML files and stylesheets that are named by the primary titles of the designs in the Figma file (i.e. buttons-and-cards.html and buttons-and-cards.css)

## User Case 1: Buttons and Cards
I'm starting with this because I did this in the previous CSS exercise and want to try to tackle this in a better way!

First step was to create all the elements in my HTML code to prepare for the CSS Grid layout:

``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="./css/buttons-and-cards.css"/>
</head>
<body>
    <header>
        <button class="seymour" id="black-button">See More</button>
        <button class="seymour" id="transp-button">See More</button>
    </header>
    <main>
        <div class="card-one">
            <div id="blackboxone">
                <div id="white-box"></div>
            </div>
            <div class="special-feature">
                <p id="spfeature">Special Feature</p>
                <a href="#">See More ></a>
            </div>
        </div>
        <div class="card-two">
            <div id="black-circle"></div>
            <h1>Title</h1>
            <h2>Subtitle</h2>
            <ul class="feature">
                <li>Feature 1</li>
                <li>Feature 2</li>
                <li>Feature 3</li>
            </ul>
            <button id="start-now">Start Now</button>
        </div>
        <div class="card-three">
            <div id="blackboxlg"></div>
            <p id="lorem">Lorem ipsum dolor sit amet consectetur adipisicing elit</p>
            <a href="#">Learn More</a>
        </div>
    </main>
</body>
</html>
```

From there, I applied basic CSS styles to confirm that the body grid container was successfully created:

``` css
body {
    display:grid;
    grid-template-rows: auto auto;
    grid-template-columns: auto;
    border: 2px black solid;
}

header {
    border: 3px greenyellow solid;
}
main {
    border: 4px purple solid;
}
```

With this done, I know I successfully created a two row grid with a single column.

Breaking down this work, I will focus on two respective areas:
1. Header Bar - contains the two See More buttons
2. Main - contains the three card build-out

### Header Bar
I will first apply the CSS styling to the "See More" button ids to properly render each according to the estimate look on the page.

I first targeted the button class as they are the same relative size and spacing and added in the padding, margin for separation, and border radius to make a curved buttion selection. The resulting code looked like:

```css
.seymour {
    padding: 15px 40px;
    margin-right: 40px;
    border-radius: 5px;
}
```

After doing so, all I needed to adjust was the background and text color of the black button, so I targeted the id "black-button" and made the appropriate changes, resulting in the completed look[^1].

```css
#black-button {
    background-color: black;
    color: white;
}
```

### Main feature

The next area to tackle were the three cards that are in the main row navigation of my grid.  The elements were all stacked on top of each other, so I applied 'display: flex' to the '<main>' element so the items would run along a horizontal main axis and applied a gap so there would be appropriate spacing between the flex child items.[^2]

```css
main {
    display: flex;
    gap: 60px;
}
```

Based on the Figma file, I didn't know if the page dynamically wrapped or now.  I interpreted this as no wrapping elements, and so applied the  'text-wrap: nowrap' property to all div elements so they would not wrap in the flex or grid containers.

```css
div {
    text-wrap: nowrap;
}
```

After this initial set up, I then broke the work out to each card:

#### Card One

The first thing I did here was create the black box, followed by the white interior box.  I selected #blackboxone and built my parameters for the size of the box.  With that created, I tested my knowledge for setting the size of #whitebox by setting the parameters of the width and height at 25%.

This worked the way I intended where the size of the white box would be 25% of the respective size of its container #blackboxone.  I then set the display for #blackboxone to flex so I could justify and align the white box to the center of the object.

```css
#blackboxone {
    display: flex;
    width: 250px;
    height: 250px;
    background-color: black;
    justify-content: center;
    align-items: center;
}
#white-box {
    width: 25%;
    height: 25%;
    border-radius: 5px;
    background-color: white;
}
```
From there, I made the edits to the .special-feature box below by creating the padding to push the content off the edges of the box, and made some font changes and margins so that the "Special Feature and See More[^3] link" would show up like the Figma model:

```css
#spfeature {
    font-size: 24px;
    margin-bottom: 50px;
}

a {
    text-decoration: none;
    color: black;
}
```

#### Card 2

I then got to work on card 2.  Immediately at looking at it, I saw that the spacing between the items were different, so a blanket use of flex and trying to justify the content with space-between would not align to the site page.

What I did instead was to make .card-two a grid instead.  This way I could control the sizes of the 5 rows of cells and then make margin, gap, and padding changes to each element to fit the different spacing setting of the elements.

This is how the code ended up:

```css
.card-two {
    display: grid;
    justify-content: center;
    text-align: center;
    grid-template-rows: auto auto auto 1fr auto;
    padding: 20px 0;
    background-color: white;
    height: 85%;
    width: 250px;
    border: black 1px solid;
}
h1 {
    font-size: 2rem;
    font-weight: 400;
    margin-top: 10px;
}
h2 {
    margin-top: 10px;
    font-size: 1rem;
    font-weight: 200;
}
.feature {
    list-style: none;
    padding: 10px 20px;
}

li {
    color: #808080;
    margin-top: 15px;
}
#start-now {
    padding: 10px 40px;
    border-radius: 5px;
    background-color: white;
}
```

#### Card 3

As I was working on building this final card, I realized that the text-wrap was messing up my whole code for the rest of the items, especially for the "lorem" placeholder text, I realized that the fix I wanted was to set flex-shrink to 0 in my flex items (div).  This fixed my unintended bug.

```css
.card-three {
    max-width: 300px;
}

#blackboxlg {
    height: 300px;
    width: 100%;
    background-color: black;
}

#cardthreetext {
    margin-top: 30px;
}
#lorem {
    font-size: 22px;
    font-family: Arial, Helvetica, sans-serif;
    margin-bottom: 20px;
}
```
The rest of this section was setting the right parameter sizes for my large black box, the paragraph text, and the link.  Once done, my site was complete!

---

## Learnings

Utilization of grids and flexbox has made manipulation of the elements and items so much easier to understand than without.  The implementation of a grid structure now allows for parent-child elements nested within one another make much more sense than the oddly implemented positioning aspect of CSS that can change based on how things are relative to one another.

I liken this to effectively making the website's landscape into a giant excel spreadsheet that you can manipulate grid tracks with, and then keep segmenting that down with flexbox or other elements as much or as little as possible.

This might have been the original intent/aim of how position was supposed to work in CSS, but because of the way relative positioning and the advent of ever shifting viewports and display sizes, this functionality seems WAY better for overall usage.


[^1]: I noticed that the fonts in the exercise are all slightly different.  In each instance of fonts, I could go around changing their font-family, but for the purposes of the grid and flexbox exercises I wanted to focus on the CSS manipulation of elements.

[^2]: One recommendation to help with understanding manipulation, especially with grid, flex, and other things, is to add borders around the different elements you're manipulating.  I find this helps me much like 'console.log' in JS.  Of course, using the browser devTools is also important, but for a quick visual look without navigating there, I find this very helpful.

[^3]: This adjustment to the link formatting also now applies to the other link in card 3, very useful! 