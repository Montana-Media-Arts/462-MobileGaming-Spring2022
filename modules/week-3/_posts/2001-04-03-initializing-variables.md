---
title: Initializing Variables
module: 3
jotted: true
---

# Initializing Variables


In larger programs, it's a good idea to declare all of the variables that are used throughout the file near the beginning. This helps us stay organized and provides a quick reference if we forget what the name of a variable was and/or if the variable had an initial value.

Following the image sheet options and setup, add these lines:
```lua

-- Initialize variables
local lives = 3
local score = 0
local died = false
 
local asteroidsTable = {}
 
local ship
local gameLoopTimer
local livesText
local scoreText
```

Let's examine each set of additions in detail:

First we declare variables to keep track of the number of lives remaining (initial value of 3), the current score (initial value of 0), and whether the player has died (initially false).

Next we declare the variable asteroidsTable which will be used for a very specific purpose throughout the game. As you recall from the previous chapter, the curly brackets ({}) indicate a Lua table (array). Among other things, tables are used to keep track of similar types of information. Since there will be many asteroids on the screen in this game, it's impractical to declare each as a unique variable such as asteroid1, asteroid2, asteroid15, etc. We need a more efficient method and that's where tables can help — essentially, tables can contain a large amount of object references and other data, growing and shrinking as needed throughout the game's life.

On the next few lines, we declare a variable placeholder for the ship object (ship), a placeholder for a timer we'll implement later, and two variables for the text objects which will display the player's remaining lives and score.

Notice that these last four declarations do not begin with any initial value or type. In Lua, this is a perfectly valid way of making a forward declaration, sometimes referred to as an upvalue. Effectively, we are telling Lua about a variable's existence, even if we don't intend to use it until later in the program.

Great! With our initial variables set, we can begin loading objects onto the screen.