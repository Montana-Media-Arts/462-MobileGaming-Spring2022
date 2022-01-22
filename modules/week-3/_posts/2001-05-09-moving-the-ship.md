---
title: Moving the ship
module: 3
jotted: true
---

# Moving the Ship

In this game, in addition to firing lasers, the player will be able to touch and drag the ship along the bottom of the screen. To handle this type of movement, we need a function to handle touch/drag events. Let's create this function in the usual manner:

```lua
ship:addEventListener( "tap", fireLaser )
 
 
local function dragShip( event )
 
 
end
```

Notice that, unlike our previous functions, this function has the keyword event in the parentheses following its name. As you learned in the BalloonTap project, Solar2D is largely an event-based framework where information is dispatched during a specific event to an event listener.

Specifically for this routine, the event parameter (table) tells us what object the user is touching/dragging, the location of the touch in content space, and a few other pieces of information. You'll see this event parameter used frequently as you move forward and study existing code samples, so it's a good idea to become familiar with it now.

Inside the function, to make things a little clearer, let's set a local variable ship equal to event.target. In touch/tap events, event.target is the object which was touched/tapped, so setting this local variable as a reference to the ship object will save us some typing as we work through the function.

```lua
local function dragShip( event )
 
    local ship = event.target
end
```

### Touch Events

Touch events, distinct from tap events, have four distinct phases based on the state of the user's touch:

- "began" — indicates that a touch has started on the object (initial touch on the screen).
- "moved" — indicates that a touch position has moved on the object.
- "ended" — indicates that a touch has ended on the object (touch lifted from the screen).
- "cancelled" — indicates that the system cancelled tracking of the touch (not to be confused with "ended").

For our convenience, let's locally set the phase (event.phase) of the touch event:

```lua

local function dragShip( event )
 
    local ship = event.target
    local phase = event.phase
end
```

With the phase locally set, we can use an if-then structure to check which phase the actual touch event is in. If it has just begun (initial touch on the ship), the "began" phase is dispatched to our function. In this conditional case, we set the touch focus on the ship — essentially, this means that the ship object will "own" the touch event throughout its duration. While focus is on the ship, no other objects in the game will detect events from this specific touch:

```lua
local function dragShip( event )
 
    local ship = event.target
    local phase = event.phase
 
    if ( "began" == phase ) then
        -- Set touch focus on the ship
        display.currentStage:setFocus( ship )
    end
end
```

Directly following this, let's store the beginning "offset" position of the touch in relation to the ship. Conceptually, as illustrated here, a touch can occur in various places within an object's bounds. In our code, event.x - ship.x gives us the horizontal offset between the exact touch point on the screen (event.x) and the ship's x position (ship.x). We set this as a property of the ship (touchOffsetX) for usage in the next phase.

```lua
    if ( "began" == phase ) then
        -- Set touch focus on the ship
        display.currentStage:setFocus( ship )
        -- Store initial offset position
        ship.touchOffsetX = event.x - ship.x
    end
end
```

For the "moved" phase (as you can guess), we move the ship! This is done by simply setting the ship's x position, but look carefully — this is where our touchOffsetX property comes into play. If we ignored this offset and simply set the ship's x position to event.x, its center axis would skip/jump to the exact touch point on the screen and, as illustrated above, the touch point within the ship bounds may not be exactly at the center. Fortunately, factoring in the offset value will produce a smooth, consistent dragging effect.

```lua
    if ( "began" == phase ) then
        -- Set touch focus on the ship
        display.currentStage:setFocus( ship )
        -- Store initial offset position
        ship.touchOffsetX = event.x - ship.x
 
    elseif ( "moved" == phase ) then
        -- Move the ship to the new touch position
        ship.x = event.x - ship.touchOffsetX
    end
end
```

### Note
For this game, ship movement will be restricted to just left and right, so we only handle changes along the x axis. If you create a game where an object can be dragged all around the screen, you should mimic this offset concept for the y axis as well. For example, in the "began" case, store the beginning y offset:

```lua
-- Store initial offset position
ship.touchOffsetX = event.x - ship.x
ship.touchOffsetY = event.y - ship.y
```

Then, in the "moved" phase, set the object's y position:

-- Move the ship to the new touch position

```lua
ship.x = event.x - ship.touchOffsetX
ship.y = event.y - ship.touchOffsetY
```

The final conditional case includes both the "ended" and "cancelled" phases. The "ended" phase indicates that the user released touch on the object, while the "cancelled" phase indicates that the system cancelled/terminated the touch event. Typically, both of these phases can be handled in the same conditional block. For this game, we simply release the touch focus on the ship:

```lua
    elseif ( "moved" == phase ) then
        -- Move the ship to the new touch position
        ship.x = event.x - ship.touchOffsetX
 
    elseif ( "ended" == phase or "cancelled" == phase ) then
        -- Release touch focus on the ship
        display.currentStage:setFocus( nil )
    end
end
```

Let's complete the dragShip() touch listener function with one more command:

```lua
    elseif ( "ended" == phase or "cancelled" == phase ) then
        -- Release touch focus on the ship
        display.currentStage:setFocus( nil )
    end
 
    return true  -- Prevents touch propagation to underlying objects
end
```

As the comment indicates, this short but important command tells Solar2D that the touch event should "stop" on this object and not propagate to underlying objects. This is essential in more complex apps where you might have multiple overlapping objects with touch event detection. Adding return true at the end of touch listener functions prevents potential (and usually undesirable) touch propagation.

### Touch Listener

We're almost finished with the movement mechanics — let's just assign the ship a "touch" event listener so that the player can touch/drag it left and right across the screen. Immediately following the dragShip() function (after its closing end statement), add the following command:

```lua
    return true  -- Prevents touch propagation to underlying objects
end
 
ship:addEventListener( "touch", dragShip )

```

Let's check the result of our code. Save your modified main.lua file, relaunch the Simulator, and experiment with touching and dragging the ship around.