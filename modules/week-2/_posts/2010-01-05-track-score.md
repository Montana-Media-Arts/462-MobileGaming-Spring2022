---
title: Track Score
module: 2
jotted: true
---

# Track Score

Congratulations, you have created a basic game in just 30 lines of code! But there is something missing, isn't there? Wouldn't it be nice if the game kept track of how many times the balloon was tapped? Fortunately that's easy to add!

First, let's create a local Lua variable to keep track of the tap count. You can add this at the very top of your existing code. In this case, we'll use it to store an integer instead of associating it with an image. Since the player should begin the game with no score, we'll initially set its value to 0, but this can change later.


```lua
local tapCount = 0
 
local background = display.newImageRect( "background.png", 360, 570 )
background.x = display.contentCenterX
background.y = display.contentCenterY
```

Next, let's create a visual object to display the number of taps on the balloon. Remember the rules of layering discussed earlier in this chapter? New objects will be placed in front of other objects which were loaded previously, so this object should be loaded after you load the background (otherwise it will be placed behind the background and you won't see it).

After the three lines which load/position the background, add the following highlighted command:

```lua
local tapCount = 0
 
local background = display.newImageRect( "background.png", 360, 570 )
background.x = display.contentCenterX
background.y = display.contentCenterY
 
local tapText = display.newText( tapCount, display.contentCenterX, 20, native.systemFont, 40 )
```

Let's inspect this command in more detail:

The command begins with local tapText which you should easily recognize as the declaration of a variable tapText.

display.newText() is another API, but instead of loading an image as we did earlier, this command creates a text object. Because we are assigning the variable tapText to this object, we'll be able to make changes to the text during our game, such as changing the printed number to match how many times the balloon was tapped.

Inside the parentheses are the parameters which we pass to display.newText(). The first parameter is the initial printed value for the text, but notice that instead of setting a direct string value like "0", we actually assign the variable which we declared earlier (tapCount). In Solar2D, it's perfectly valid to specify a variable as a parameter of an API, as long as it's a valid variable and the API accepts the variable's type as that parameter.

The second two parameters, display.contentCenterX and 20, are used to position this text object on the screen. You'll notice that we use the same shortcut of display.contentCenterX to position the object in the horizontal center of the screen, and 20 to set its vertical y position near the top of the screen.

The fourth parameter for this API is the font in which to render the text. Solar2D supports custom fonts across all platforms, but for this game we'll use the default system font by specifying native.systemFont.

The final parameter (40) is the intended size of the rendered text.


Let's check the result of this new code. Save your modified main.lua file and relaunch the Simulator. If all went well, the text object should now be showing, positioned near the top of the screen.

Continuing with our program — by default, text created with display.newText() will be white. Fortunately, it's easy to change this. Directly following the line you just added, type the highlighted command:

```lua
local tapText = display.newText( tapCount, display.contentCenterX, 20, native.systemFont, 40 )
tapText:setFillColor( 0, 0, 0 )
```

Simply put, this setFillColor() command modifies the fill color of the object tapText. The setFillColor() command accepts up to four numeric parameters in the range of 0 to 1, one each for the color channels red, green, blue, and alpha. In this game, we're filling the object with solid black, so the first three channels are set to 0 (alpha defaults to 1 and it can be omitted in this case).

Let's move on! The new text object looks nice, but it doesn't actually do anything. To make it update when the player taps the balloon, we'll need to modify our pushBalloon() function. Inside this function, following the balloon:applyLinearImpulse() command, insert the two highlighted lines:

```lua
local function pushBalloon()
    balloon:applyLinearImpulse( 0, -0.75, balloon.x, balloon.y )
    tapCount = tapCount + 1
    tapText.text = tapCount
end
```

Let's examine these lines individually:

The tapCount = tapCount + 1 command increases the tapCount variable by 1 each time the balloon is tapped.

The second new command, tapText.text = tapCount, updates the text property of our tapText object. This allows us to quickly change text without having to create a new object each time.