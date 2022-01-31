---
title: Lives and Score
module: 3
jotted: true
---

# Lives and Score

Now let's place UI labels for the player's lives and score on the screen:

```lua

-- Display lives and score
local uiGroup = display.newGroup()
livesText = display.newText( "Lives: " .. lives, 200, 80, native.systemFont, 36 )
scoreText = display.newText( "Score: " .. score, 400, 80, native.systemFont, 36 )
uiGroup:insert(livesText)
uiGroup:insert(scoreText)
```

To keep things simple, we use a special Lua method with the labels to show our lives and score. Placing two periods together in Lua (..) is called concatenation. Concatenation joins two strings into one. Thus, in the livesText = display.newText() command above, we are joining the string Lives: and the variable lives for a result of Lives: 3 being displayed on the screen (remember that we set the initial value of lives to 3 earlier). Similarly, for scoreText, we join the string Score: and the variable score for a result of Score: 0.


Let's check the result of our code so far. Save your modified main.lua file and relaunch the Simulator. If all went well, the background, ship, and text labels should now be showing on the screen.

Everything looks good so far except for the slightly distracting status bar at the top of the screen. On mobile devices, this system-generated element usually displays various information like the strength of the cellular/WiFi connection, the time, the remaining battery life, etc. While this information is valuable for general usage of the device, it can be distracting when the user is playing a game. To hide the status bar, add the following:

```lua
-- Hide the status bar
display.setStatusBar( display.HiddenStatusBar )
```

Finally, let's write a function to update the text property of both livesText and scoreText. This will be similar to the function we wrote in the previous chapter. As you recall, any time you create a new label or object with display.newText(), the text's label/value is stored in the text property of the object, so we update that property with the concatenated string value of the label and its associated variable.

```lua
local function updateText()
    livesText.text = "Lives: " .. lives
    scoreText.text = "Score: " .. score
end
```

Now that we have the basic visual objects in place, can load images from the image sheet, and update the UI labels for both lives and score, we're ready to get started on the game logic and events!