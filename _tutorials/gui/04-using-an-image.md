---
tutorial: Gui Tutorial
layout: step-abstract
title: Using an Image
position: 4
---

### Using an image

For this section we'll use this image as the texture for our button.\
It's dimensions are `64`x`72`pixels.\
![upThink.png](/assets/img/gui-tutorial/upThink.png)


<div class="note">For this example we'll be saving the image to <code>~/images</code> however you can put it wherever you like.</div>

To make this change we can replace this line
```lua
local button = myGui.newRectangle(5,5,20,12)
button.setColor( 0xFFFFFFFF ) --opaque white, 0x FF FF FF FF
```

with this
```lua
local button = myGui.newImage("~/images/upThink.png",5,5,20,12)
```

<div class="note">If you're following along in REPL, you can do <code>button.remove()</code> to remove the current rectangle before making the image.</div>

and if we open it now...
![gui with distorted image](/assets/img/gui-tutorial/gui-4-1.png)
<span style="text-decoration:line-through">We can see</span>\
<span style="font-size:50%">64 / 72 * 20 = 17.7</span>
```lua
button.setSize(20,17)
```
![gui with distorted image](/assets/img/gui-tutorial/gui-4-2.png)
We can see our image on the button.