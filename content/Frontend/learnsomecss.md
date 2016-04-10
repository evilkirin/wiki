---
title: "Learn You Some CSS"
date: 2016-01-17 13:11
---

> 要学前端，CSS是必经之路，就不要怕麻烦了。

# [Learn CSS Layout](http://learnlayout.com/)

- the `display` property
    + display is CSS's most important property for controlling layout
    + block, inline, none, line-block, flex
- So, talking about block-level elements:
    + setting the width to 600px is not enough
        * margin: 0 auto
        * even better -> max-width: 600px
    + the weird box model
        * the element's border and padding will stretch out the element beyond the specified width.
        * and `box-sizing: border-box` come to rescue
- In order to make more complex layouts, we need to discuss the __position__ property
    + static
        * default value
        * A static element is said to be not positioned and an element with its position set to anything else is said to be positioned
    + relative
        * behaves the same as static unless you add some extra properties
        * A fixed element is positioned relative to the viewport
    + absolute
        * behaves like fixed except relative to the nearest positioned ancestor instead of relative to the viewport
- `float: left`
    + intended for wrapping text around images
    + clear
    + **clearfix**
        * `overflow: auto`
        * `zoom: 1`
- percent width
    + yes, just width
    + Percent is a measurement unit relative to the containing block
    + percent width layout
        * but it couldn't handle it when the window or layout is too narrow
- media queries
    + @media screen and (min-width:600px)
- `display: inline-block`
    + inline-block elements are like inline elements but they can have a width and height
    + layout
        * affected by `vertical-align`
        * needs to set width for all columns
        * There will be a gap between the columns if there is any whitespace between them in the HTML
- column -> let you easily make multi-column text
    + column-count
    + column-gap
- `display: flex`
    + `flex: 1`
    + align-items
    + justify-content

# So, questions remain...

- what exactly is block-level elements, how does it differ from other type of display type.
- this is all about flexbox?

- [CSS Layout - The display Property](http://www.w3schools.com/css/css_display_visibility.asp)
    + block-level elements
        * A block-level element always starts on a new line and takes up the full width available (stretches out to the left and right as far as it can).
    + inline elements
        * An inline element does not start on a new line and only takes up as much width as necessary
- [CSS Layout - Horizontal Align](http://www.w3schools.com/css/css_align.asp)
    + Center align
        * `margin: auto`
    + Left and Right Align
        * using postion: absolute
        * using float
- [CSS Pseudo-classes](http://www.w3schools.com/css/css_pseudo_classes.asp)
    + A pseudo-class is used to define a special state of an element
- [CSS Pseudo-elements](http://www.w3schools.com/css/css_pseudo_elements.asp)
    + A CSS pseudo-element is used to style specified parts of an element