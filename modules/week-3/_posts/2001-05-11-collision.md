---
title: Collision
module: 3
jotted: true
---

# Collision

Time to handle collisions! Initially, we're only going to detect specific collisions:

When a laser collides with an asteroid.
When an asteroid collides with the ship.
Collisions are reported between pairs of objects, and they can be detected either locally on an object, using an object listener, or globally using a runtime listener. Different games require different methods, but here's a general guideline:

Local collision handling is best utilized in a one-to-many collision scenario, for example one player object which may collide with multiple enemies, power-ups, etc.

Global collision handling is best utilized in a many-to-many collision scenario, for example multiple hero characters which may collide with multiple enemies.

While this game has just one player object (the ship), it might seem that the best choice is local collision handling. However, the game will also need to detect collisions between multiple lasers and multiple asteroids, so global collision handling is a better option.

### Restoring the Ship

Before we get into collision handling, we need a function that can be called to restore the ship following collision with an asteroid. In our game, we'll mimic classic arcade games where, as the new ship fades into view, it's temporarily invincible — after all, it wouldn't be fair to allow players to die consecutive times without being given a chance to dodge incoming asteroids!

Following the code you've already written, add the following highlighted function:

```lua
gameLoopTimer = timer.performWithDelay( 500, gameLoop, 0 )
  
local function restoreShip()
 
    ship.isBodyActive = false
    ship.x = display.contentCenterX
    ship.y = display.contentHeight - 100
 
    -- Fade in the ship
    transition.to( ship, { alpha=1, time=4000,
        onComplete = function()
            ship.isBodyActive = true
            died = false
        end
    } )
end
```

Let's examine the content of this function:

The first command, ship.isBodyActive = false, effectively removes the ship from the physics simulation so that it ceases to interact with other bodies. We do this (temporarily) so that, as the ship fades back into view, colliding asteroids will not trigger another collision response.

The next two lines simply reposition the ship at the bottom-center of the screen.

The final command might not make complete sense right now, but it will after we add "death" functionality further down. Essentially, this transition.to() command fades the ship back to full opacity (alpha=1) over the span of four seconds. It also includes an onComplete callback to an anonymous function. This function restores the ship as an active physical body and resets the died variable to false.

Collision Function
Next, let's write the foundation of our collision function:

```lua
        end
    } )
end
 
 
local function onCollision( event )
 
    if ( event.phase == "began" ) then
 
        local obj1 = event.object1
        local obj2 = event.object2
    end
end
```

This is relatively simple and you should recognize some basic concepts from earlier:

Similar to touch events, collisions have distinct phases, in this case "began" and "ended". The "began" collision phase is by far the most common phase you'll need to handle, but there are instances where detecting the "ended" phase is important. Don't worry too much about this now — here, we simply isolate the "began" phase by wrapping our functionality in a conditional clause.

For simplicity throughout the function, we reference the two objects involved in the collision with the local variables obj1 and obj2. When detecting collisions with the global method, these objects are referenced by event.object1 and event.object2.

### Lasers and Asteroids

Let's handle our first collision condition: lasers and asteroids. Remember how we assign a myName property to each object when we create it? This property now becomes critical as a means to detect which two object types are colliding. Here, the opening conditional clause checks the myName property of both obj1 and obj2. If these values are "laser" and "asteroid", we know which two object types collided and we can proceed with handling the outcome.

```lua
    if ( event.phase == "began" ) then
 
        local obj1 = event.object1
        local obj2 = event.object2
 
        if ( ( obj1.myName == "laser" and obj2.myName == "asteroid" ) or
             ( obj1.myName == "asteroid" and obj2.myName == "laser" ) )
        then
 
        end
    end
end
```

When detecting collisions with the global method, there is no way to determine which is the "first" and "second" object involved in the collision. In other words, obj1 may be the laser and obj2 the asteroid, or they might be flipped around. This is why we build a multi-conditional clause to detect both possibilities.

Inside the conditional clause, let's begin by simply removing the two objects via display.remove(). While a fancy explosion effect would be awesome, this project merely exhibits how to handle collisions — how you expand on this later depends on your imagination!

```lua
        if ( ( obj1.myName == "laser" and obj2.myName == "asteroid" ) or
             ( obj1.myName == "asteroid" and obj2.myName == "laser" ) )
        then
            -- Remove both the laser and asteroid
            display.remove( obj1 )
            display.remove( obj2 )
        end
    end
end
```

Next, let's remove the destroyed asteroid from the asteroidsTable table so that the game loop doesn't need to worry about it any further. For this task, we use another for loop which iterates through asteroidsTable, locates the instance of the asteroid, and removes it:

```lua
        if ( ( obj1.myName == "laser" and obj2.myName == "asteroid" ) or
             ( obj1.myName == "asteroid" and obj2.myName == "laser" ) )
        then
            -- Remove both the laser and asteroid
            display.remove( obj1 )
            display.remove( obj2 )
 
            for i = #asteroidsTable, 1, -1 do
                if ( asteroidsTable[i] == obj1 or asteroidsTable[i] == obj2 ) then
                    table.remove( asteroidsTable, i )
                    break
                end
            end
        end
    end
end
```

In this loop, we also utilize a minor efficiency trick known as breaking, executed by the break command. Because we're only looking for one specific asteroid, the loop can immediately break/stop once that asteroid has been removed, effectively stopping any further processing effort.

Finally, to reward the player for destroying an asteroid, we'll increase the score variable by 100 and update the scoreText text object to reflect the new value:

```lua
        if ( ( obj1.myName == "laser" and obj2.myName == "asteroid" ) or
             ( obj1.myName == "asteroid" and obj2.myName == "laser" ) )
        then
            -- Remove both the laser and asteroid
            display.remove( obj1 )
            display.remove( obj2 )
 
            for i = #asteroidsTable, 1, -1 do
                if ( asteroidsTable[i] == obj1 or asteroidsTable[i] == obj2 ) then
                    table.remove( asteroidsTable, i )
                    break
                end
            end
 
            -- Increase score
            score = score + 100
            scoreText.text = "Score: " .. score
        end
    end
end
```

### Asteroids and the Ship

Now let's handle the second collision condition: asteroids and the ship. Add the following condition to the if-then statement following the first one. Notice that we use elseif because we're adding another possible condition to the same statement:

```lua
            -- Increase score
            score = score + 100
            scoreText.text = "Score: " .. score
 
        elseif ( ( obj1.myName == "ship" and obj2.myName == "asteroid" ) or
                 ( obj1.myName == "asteroid" and obj2.myName == "ship" ) )
        then
 
        end
    end
end
```

Inside this conditional clause, let's begin with an additional if-then check:

```lua
        elseif ( ( obj1.myName == "ship" and obj2.myName == "asteroid" ) or
                 ( obj1.myName == "asteroid" and obj2.myName == "ship" ) )
        then
            if ( died == false ) then
 
            end
        end
    end
end
```

This conditional check might seem a little strange, but we need to confirm that the ship has not already been destroyed. As the game progresses, or with a faster asteroid spawning rate, it's entirely possible that the ship will be struck by two asteroids almost simultaneously. Losing two lives in that case obviously isn't fair, so we check the value of died and only proceed if it's false.

Inside this if-then clause, let's immediately set died = true because the player actually has died this time!

```lua

elseif ( ( obj1.myName == "ship" and obj2.myName == "asteroid" ) or
                 ( obj1.myName == "asteroid" and obj2.myName == "ship" ) )
        then
            if ( died == false ) then
                died = true
            end
        end
    end
end
```

Following this, we'll subtract a life from the lives variable and update the livesText text object to reflect the new value:

```lua
        elseif ( ( obj1.myName == "ship" and obj2.myName == "asteroid" ) or
                 ( obj1.myName == "asteroid" and obj2.myName == "ship" ) )
        then
            if ( died == false ) then
                died = true
 
                -- Update lives
                lives = lives - 1
                livesText.text = "Lives: " .. lives
            end
        end
    end
end
```

Finally, let's include a conditional statement to check if the player is out of lives:

```lua
        elseif ( ( obj1.myName == "ship" and obj2.myName == "asteroid" ) or
                 ( obj1.myName == "asteroid" and obj2.myName == "ship" ) )
        then
            if ( died == false ) then
                died = true
 
                -- Update lives
                lives = lives - 1
                livesText.text = "Lives: " .. lives
 
                if ( lives == 0 ) then
                    display.remove( ship )
                else
                    ship.alpha = 0
                    timer.performWithDelay( 1000, restoreShip )
                end
            end
        end
    end
end
```

In the opening clause of this statement, if lives is equal to 0, we simply remove the ship entirely. This is the point where you could show a "game over" message or perform some other action, but for now we'll leave the possibilities open.

In the default else clause (the player has at least one life remaining), we make the ship invisible by setting its alpha property to 0. This ties into the restoreShip() function which we wrote earlier where, when the ship fades back into view, the transition.to() command transitions the ship's alpha back to 1. Immediately following that line, we actually call the restoreShip() function after a delay of one second — this yields a slight delay before the ship begins to fade back into view.

### Collision Listener

All of our collision logic is now in place, but absolutely nothing will happen unless we link it up! Since we decided to implement collisions in the global method, it only takes one command to tell Solar2D that it should listen for new collisions during every runtime frame of the app.

Immediately following the onCollision() function (after its closing end statement), add the following command:

```lua
        end
    end
end
 
Runtime:addEventListener( "collision", onCollision )
```

This command is similar to previous event listeners where we added a "tap" or "touch" listener type to a specific object. Here, we simply add a "collision" listener type to the global Runtime object.

That's it! Save your main.lua file, relaunch the Simulator, and your game will be finished — the player has full control over the ship, asteroids continue to spawn and move across the screen, score and lives are accounted for, and we basically have a fully functioning game!