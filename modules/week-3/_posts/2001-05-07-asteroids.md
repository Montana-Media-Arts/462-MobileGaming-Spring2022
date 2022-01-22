---
title: Asteroids
module: 3
jotted: true
---

# Creating Asteroids

The creation of asteroids will be handled by a function. This function will be run (called) on a regular basis as part of our game loop, a function which is called on a repeating basis to handle various game functionality.

Like our previous functions, we begin with local function followed by the name of the function and a pair of parentheses. Naturally, we also close the function with an end command:

```lua
local function updateText()
    livesText.text = "Lives: " .. lives
    scoreText.text = "Score: " .. score
end
 
 
local function createAsteroid()
 
 
end
```

Inside the function, we begin by creating a new instance of an asteroid named newAsteroid, prefaced with local as usual. The object itself is an image just like everything else we've created so far, taken from the same image sheet (objectSheet) that we loaded earlier:

```lua
local function createAsteroid()
 
    local newAsteroid = display.newImageRect( mainGroup, objectSheet, 1, 102, 85 )
end
```

Since there will be a lot of asteroids on the screen at any given time, we need a way to keep track of them. As you recall from the previous chapter, we initialized several variables, among them the table named asteroidsTable. This table now comes into play as a place to store the new asteroid. To insert the new asteroid instance into the table, we can use the built-in Lua table.insert() command. This command just requires the name of the table (asteroidsTable) and the object/value to insert, in this case the newAsteroid object we just created:

```lua
local function createAsteroid()
 
    local newAsteroid = display.newImageRect( mainGroup, objectSheet, 1, 102, 85 )
    table.insert( asteroidsTable, newAsteroid )
end
```

With the asteroid image now loaded and placed into the table, we can add it to the physics engine:

```lua
local function createAsteroid()
 
    local newAsteroid = display.newImageRect( mainGroup, objectSheet, 1, 102, 85 )
    table.insert( asteroidsTable, newAsteroid )
    physics.addBody( newAsteroid, "dynamic", { radius=40, bounce=0.8 } )
end
```
### Note
As with the ship object in the previous chapter, we're taking a shortcut by adding a circular physics body (radius=40) to all asteroids, even though the asteroid image isn't exactly circular. In time, you'll learn how to add an accurate shape-based physics body to any object.

Finally, let's assign the asteroid a myName property of "asteroid". Later, when detecting collisions, it will simplify things to know that this object is an asteroid.

```lua
local function createAsteroid()
 
    local newAsteroid = display.newImageRect( mainGroup, objectSheet, 1, 102, 85 )
    table.insert( asteroidsTable, newAsteroid )
    physics.addBody( newAsteroid, "dynamic", { radius=40, bounce=0.8 } )
    newAsteroid.myName = "asteroid"
end
```

## Placement

Now that we have a new asteroid on the screen, let's set its point of origin. For our game, asteroids will come from the left, right, or top of the screen — it wouldn't be fair to have an asteroid sneak up from behind!

Given three possible points of origin, we need Lua to generate a random integer between 1 and 3. This is easily done using the math.random() command with a sole parameter of 3:

```lua
    local newAsteroid = display.newImageRect( mainGroup, objectSheet, 1, 102, 85 )
    table.insert( asteroidsTable, newAsteroid )
    physics.addBody( newAsteroid, "dynamic", { radius=40, bounce=0.8 } )
    newAsteroid.myName = "asteroid"
 
    local whereFrom = math.random( 3 )
end
```

Following this command, the local variable whereFrom will have a value of either 1, 2, or 3. Using this, we can implement a conditional if-then structure to handle each of the three cases. In Lua, the structure begins in this basic form:

```lua
    local whereFrom = math.random( 3 )
 
    if ( whereFrom == 1 ) then
 
    end
end
```
### Notes
Observe an important distinction about the Lua language: when you are assigning a value to a variable, you use a single equal sign (=). However, if you are doing a comparison in a conditional statement, you must use two equal signs (==) to indicate that you are checking for equality instead of assigning a value.

To tell Lua that you're finished with a conditional structure, use the keyword end.

The parentheses around the comparison are optional, but many programmers use them for clarity or to build more complex multi-condition statements.


Let's use this first condition, whereFrom == 1, to place an asteroid slightly off the left edge of the screen. Insert three lines so that your conditional block looks like this:

```lua
    if ( whereFrom == 1 ) then
        -- From the left
        newAsteroid.x = -60
        newAsteroid.y = math.random( 500 )
    end
end
```
Since this asteroid will come from the left side, we set its x property to -60. This should be a sufficient amount to ensure that not even a portion of the asteroid is visible to the player when it's first created (it's entirely off screen). As for the y property, we use math.random() once again to randomly select a value between 1 and 500, effectively making the asteroid appear somewhere between the top of the content area and about half the distance down — after all, we don't want any asteroids coming from a place that makes it impossible to shoot them!

### Movement
Now that we have the starting point, we need to tell the asteroid where it should move to. This time we're going to use another physics command: object:setLinearVelocity(). This command is similar to the object:applyLinearImpulse() command which we used in the previous project, but instead of applying a sudden "push" to the object, it simply sets the object moving in a steady, consistent direction.

Add the highlighted line directly following the previous lines:

```lua
    if ( whereFrom == 1 ) then
        -- From the left
        newAsteroid.x = -60
        newAsteroid.y = math.random( 500 )
        newAsteroid:setLinearVelocity( math.random( 40,120 ), math.random( 20,60 ) )
    end
end
```

This might look complicated, but object:setLinearVelocity() simply requires two numbers indicating the velocity in the x and y directions respectively. The only twist we're using here is math.random() to randomize the values so that each asteroid moves in a slightly different direction.

Notice that we call math.random() with two parameters this time, while before we called it with just one. When called with one parameter, the command randomly generates an integer between 1 and the value you indicate. When called with two parameters, the command randomly generates an integer between the two specified values, for example between 40 and 120 in the first instance above.

If we decided to call/run this function now, we might see an asteroid slowly moving across the screen from the left side, but probably not. Why? Because we haven't added conditional cases for the other two sides of the screen! Remember, Lua is randomly choosing a number between 1 and 3, but currently we're only handling the occurrence of 1, so there's just ⅓ chance that our current code will generate an asteroid.

The following two conditions will complete the three possible sides from which asteroids can originate. When adding multiple conditions into the same if-then structure, those following the first condition should begin with elseif, not with if. Observe these additions:

```lua
    if ( whereFrom == 1 ) then
        -- From the left
        newAsteroid.x = -60
        newAsteroid.y = math.random( 500 )
        newAsteroid:setLinearVelocity( math.random( 40,120 ), math.random( 20,60 ) )
    elseif ( whereFrom == 2 ) then
        -- From the top
        newAsteroid.x = math.random( display.contentWidth )
        newAsteroid.y = -60
        newAsteroid:setLinearVelocity( math.random( -40,40 ), math.random( 40,120 ) )
    elseif ( whereFrom == 3 ) then
        -- From the right
        newAsteroid.x = display.contentWidth + 60
        newAsteroid.y = math.random( 500 )
        newAsteroid:setLinearVelocity( math.random( -120,-40 ), math.random( 20,60 ) )
    end
end
```

With these lines, all three conditions are properly accounted for. Now, when this function is called/run, an asteroid will randomly appear in one of the three specified regions and begin moving across the screen.

### Rotation
Let's wrap up the createAsteroid() function with an additional command for visual interest. To make the asteroids slowly rotate about their central point as they move through space, we can apply a random amount of torque (rotational force). Following the if-then structure (after its closing end statement), add the following highlighted command:

```lua
    elseif ( whereFrom == 3 ) then
        -- From the right
        newAsteroid.x = display.contentWidth + 60
        newAsteroid.y = math.random( 500 )
        newAsteroid:setLinearVelocity( math.random( -120,-40 ), math.random( 20,60 ) )
    end
 
    newAsteroid:applyTorque( math.random( -6,6 ) )
end
```