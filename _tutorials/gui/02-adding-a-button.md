---
tutorial: Gui Tutorial
layout: step-abstract
title: Adding a button
position: 2
---

Lets add a button
```lua
local button = myGui.newRectangle( 5, 5, 20, 12 ) --x,y,width,height
```

If you open the gui now you will see a black rectangle.
Exciting, but it's not a button so lets make it more button like.

<div class="note">The colors here are defined using the hex values, however if you like you can set them using <code>{r,g,b}</code> or <code>{r,g,b,a}</code> as well.<br>If using either table form, values are <code>0</code> to <code>1</code></div>
<div class="note">The <code>x</code>,<code>y</code>,<code>width</code>, and <code>height</code> args use Minecraft's scaled pixels, these are larger than the actual pixels on your monitor.</div>
### Changing the background
```lua
rect.setColor( 0xFFFFFFFF ) --opaque white, 0x FF FF FF FF
```

### Making it change color when you hover it
```lua
button.setHoverTint( 0x440044FF ) --transparent blue 0x 44 00 44 FF
```

### Opened again
![white rectangle gui](/assets/img/gui-tutorial/gui-2-1.gif)
Looking much better, but it still doesn't do anything yet.

Our fancy rectangle fails to meet our aspirations. 

### Making it do something
To really make it a button, it has to do something when it's clicked, so lets do that.

```lua
button.setOnMouseClick(function()
    toast("Click!", "You clicked the button")
end)
```
![white rectangle gui](/assets/img/gui-tutorial/gui-2-2.png)