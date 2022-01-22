---
title: Load Background
module: 2
jotted: false
---

# Balloon Project

## Loading the Background

The first image that we need to load is the background. Solar2D places everything on the screen from back to front in regards to layering, so the first image we load will exist behind other images that are loaded afterward. While there are ways to change the layering order of images and send them to the back or front of the display stack, we'll keep this project simple and load them in a logical order.

Using your chosen text editor, locate and open the main.lua file within your project folder. The main.lua file is the foundational "core program file" of every Solar2D project and you cannot create an app without it. This is the Lua file with which the application starts, every time you run the app.

In this main.lua file, type in the highlighted command:
```lua
-----------------------------------------------------------------------------------------
--
-- main.lua
--
-----------------------------------------------------------------------------------------
 
local background = display.newImageRect( "background.png", 360, 570 )
```

There are a several aspects involved with this command. Let's break it down:

The first word, local, is a Lua command indicating that the next word will be a variable. A variable, just like you learned in math class, is used to store a value. In this case, that value will be an image used as your background.
Note that local is always lowercase and it's used here to declare a variable; for example, the first time you use the variable, you should add the word local in front of it.

The second word, background, is the name of our variable. Any time we want to make changes to the image stored in background, we will use this variable name.
Remember to always use different variable names each time you use a variable. Just as it gets confusing if everyone in a classroom is named "John," using the same variable name for all of your objects creates confusion in your program.

The = (equal sign) is used to assign the variable background to an image.

**display.newImageRect()** is one of the Solar2D APIs. It is used to load an image from a file so that you can use it in the app. There are a couple of ways to load an image into your app, but display.newImageRect() is special in that it can resize/scale the image (this will be explained in just a moment).

Inside the parentheses are the parameters which we pass to display.newImageRect(), sometimes referred to as arguments. The first parameter is the name of the image file that we want to load, including the file extension (.png).

The specified name must match the actual file name exactly, including case-sensitive matching! For instance, if the actual file name is background.png, do not enter it as "BackGround.PNG".

The next two parameters, 360 and 570 specify the size that we want the background image to be. In this case, we'll simply use the image's pixel dimensions, although as noted above, display.newImageRect() allows you to resize/scale the image via these numbers.

The final step for the background is to position it at the correct location on the screen. Immediately following the line you just entered, add the two highlighted commands:

```lua
local background = display.newImageRect( "background.png", 360, 570 )
background.x = display.contentCenterX
background.y = display.contentCenterY
```

By default, Solar2D will position the center of an object at the coordinate point of 0,0 which is located in the upper-left corner of the screen. By changing the object's x and y properties, however, we can move the background image to a new location.

For this project, we'll place the background in the center of the screen — but what if we don't know exactly which coordinate values represent the center? Fortunately, Solar2D provides some convenient shortcuts for this. When you specify the values display.contentCenterX and display.contentCenterY, Solar2D will set the center coordinates of the screen as the background.x and background.y properties.

Let's check the result of your code! Save your modified main.lua file and then, from within the Simulator, "relaunch" it using ⌘-R (Command-R). If all went well, the background should now be showing, centered on the screen.

If you get an error or can't see the background, there are a few possibilities as to the cause:

* One of the commands was typed incorrectly.
* The image file isn't in the same folder as main.lua.
* The specified filename and/or extension is incorrect or mismatched in case.
* Remember that the Simulator Console window is a valuable place to check for and diagnose potential errors in your code. On Windows, this panel is always accessible in the Simulator. On Mac, if this window isn't already open, you can view it by selecting Window → Console.

