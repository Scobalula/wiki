---
title: LUI Element Positioning
keywords: blackops3, lui
last_updated: 12th January 2020
credits: [Blak]
summary: "This is a guide on how to position UIElements in LUI."
sidebar: black_ops_3_sidebar
permalink: black_ops_3/lui_element_positioning.html
folder: black_ops_3
---

## Pretext
Element positioning is possible one of the most annoying things, at time of writing, to learn in LUI as a beginner. However, I believe this can be primarily attributed to a lack of reference & lack of guidance out there for setting up element positioning. What a convenient opportunity to write a guide on it!

This guide will go through basic Left/Right/Top/Bottom anchored positioning, as well as central positioning and double anchoring.

## Basic principles
Key points:
* In LUI, the display is 1280x720.
* Anchors will apply to the boundaries of the parent element.
* Positioning beyond the boundaries of the parent element is possible.

To define the boundaries of your UIElement, you use the two following functions:
```lua
Element:setLeftRight(anchorLeft, anchorRight, startPosition, endPosition) --Define the anchors for left and right position, and the start end positions.
Element:setTopBottom(anchorTop, anchorBottom, startPosition, endPosition) --Define the anchors for top and bottom position, and the start end positions.
```

## Ok wonderful, what does this actually mean though?
First let's focus on the anchor arguments.

If you set one anchor to true & one to false on each function call, your element's Start & End positions will be relative to whichever anchor is true. So for example, if my `setTopBottom` was true & false, my Start & End positions would be offsetted from the top of the parent widget/menu. For now, think of your element as a dot. By setting a top anchor, it's now positioned at the top, and the principle is the same for all other anchors.

If you set neither anchor to true, your element will centre align. You can then have one position be negative, one be positive and both be half of your intended element width. To align off centre, follow the graphic further down.

Then finally, there's the double anchor. For this, both anchors are set to true. This will then position the element to fill the entire boundaries of the parent element, unless you apply start & end positions. The way you do this is a little different, and will be covered later in the guide.

## Graphic: How does Start / End position offsetting work?
{% include note.html content="This does not apply to double anchoring in the exact same way." %}

![](https://i.gyazo.com/064dcc6e1787b803beabd38340e5ed0d.png)

So, to explain:

### Positive positioning
Let's go with my original example of my widget set to a top anchor (`Element:setTopBottom(true, false, 0, 0)`). Right now, it's positioned at the top of my parent widget and has no height.

To now give it height, I need to define its start & end positions. I want it positioned 24px from the top of the widget, and for it to be 24px in height. For this, I need to do a little bit of calculating:

`end position = start position + intended height`

So 24 is my start position, and 24+24 is 48, which is my end position. So I enter that into my `setTopBottom` call:

`Element:setTopBottom(true, false, 24, 48)`

So now my element is 24px from the top of the parent element, and 24px in height.

### Negative positioning
Now I've decided that I want my element to be rightwardly aligned too `false, true`. I want it 30px from the widget boundary to the left, and it to be 50px in width.]

As shown from the graphic above, positive positioning will always move the element to the right, but negative positioning will move it leftward, so let's use negative positioning.

`start position = end position - intended width`

In this case end position is negative my initial offset from the parent element boundary (-30px). And -30-50=-80, which is my start position. Now to put that into the function call:

`Element:setLeftRight(false, true, -80, -30)`

### Central positioning
On another element, I want it centre aligned with width 90px. Ok, half 90 to get 45. Then, it's simply:

`Element:setLeftRight(false, false, 45, -45)`

It's the same as if it were anchored, except for the offsets being based on a point in the centre.

### Double anchor positioning

Double anchoring is different in that the Start position applies from the left anchor position, and the End position applies from the right anchor position. I want my element to be 3px from the left boundary, and 2px from the right boundary. So, to move it 3 to the right from the left, that's just 3. Then, to move it 2 to the left from the right boundary, that's -2px.

`Element:setLeftRight(true, true, 3, -2)`
