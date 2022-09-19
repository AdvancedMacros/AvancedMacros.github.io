---
tutorial: Gui Tutorial
layout: step-abstract
title: Making it better
position: 3
---

At this point our button is still very basic, and there's no way to tell what this button is for.

Once again our fancy rectangle fails to meet our aspirations...<br>
...so lets make it better

### For reference
The current code should look something like this:
```lua
local myGui = gui.new()
local button = myGui.newRectangle(5,5,20,12)
button.setColor( 0xFFFFFFFF ) --opaque white, 0x FF FF FF FF
button.setHoverTint( 0x440044FF ) --transparent blue 0x 44 00 44 FF
button.setOnMouseClick(function()
    toast("Click!", "You clicked the button")
end)
myGui.open()
```

### Styling the button
There's two ways we can go about styling our button right now, we can either use an image texture so it looks exactly how we want.
The alternative is to write some more code to add things like outlines and text to our button.