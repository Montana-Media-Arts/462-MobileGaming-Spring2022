---
title: Functions
module: 2
jotted: true
---

## Functions

At this point, we have a balloon that drops onto a platform and bounces slightly. That's not very fun, so let's make this into a game! For our balloon tap game to work, we need to be able to push the balloon up a little each time it's tapped.

To perform this kind of feature, programming languages use what are called functions. Functions are short (usually) sections of code that only run when we tell them to, like when the player taps the balloon.

Let's create our first function:

```lua
local function pushBalloon()
 
end
```

Functions are essential for both app and game development, so let's examine the basic structure:

As before, we use the keyword local to declare the function.

The keyword function tells Solar2D that this is a function and that its set of commands will be called by the name pushBalloon.

The ending parentheses (()) are required. In later chapters we will put something inside these parentheses, but for now you can leave this as shown.

As mentioned above, functions are self-contained sections (blocks) of code which run only when we tell them to. Thus, whenever you create a function, you must close it with the keyword end. This tells Lua that the function is finished.

Excellent, we now have a function! However, it's currently an empty function so it won't actually do anything if we run it. Let's fix that by adding the following line of code inside the function, between where we declare the function (its opening line) and the closing end keyword:

```lua
local function pushBalloon()
    balloon:applyLinearImpulse( 0, -0.75, balloon.x, balloon.y )
end
```

It's considered good programming practice to indent at least one tab or 3-4 spaces when you add lines of code inside functions. This makes your code more readable and it's easier to recognize functions in longer programs.

balloon:applyLinearImpulse is a really cool command. When applied to a dynamic physical object like the balloon, it applies a "push" to the object in any direction. The parameters that we pass tell the physics engine how much force to apply (both horizontally and vertically) and also where on the object's body to apply the force.

The first two parameters, 0 and -0.75, indicate the amount of directional force. The first number is the horizontal, or x direction, and the second number is the vertical, or y direction. Since we only want to push the balloon upwards (not left or right), we use 0 as the first parameter. For the second parameter, with a value of -0.75, we tell the physics engine to push the balloon up a little bit. The value of this number determines the amount of force that is applied: the bigger the number, the higher the force.


As shown in the diagram at right, positive x values in Solar2D extend to the right, while positive y values extend downward (not upward as in the Cartesian coordinate system). This is why we use a negative value (-0.75) to push the balloon upward.

The third and fourth parameters, balloon.x and balloon.y, tell the physics engine where to apply the force, relative to the balloon itself. If you apply the force at a location which is not the center of the balloon, it may cause the balloon to move in an unexpected direction or spin around. For this game, we will keep the force focused on the center of the balloon.

That's it! We could, if needed, add additional commands inside the pushBalloon() function, but for this simple game, we only need to push the balloon upward with a small amount of force.
