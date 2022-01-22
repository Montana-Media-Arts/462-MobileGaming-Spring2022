---
title: Loading the Platform
module: 2
jotted: false
---

## Loading the Platform

Time to load the platform. This is very similar to loading the background. Following the three lines of code you've already typed, enter the following highlighted commands:

```lua
local background = display.newImageRect( "background.png", 360, 570 )
background.x = display.contentCenterX
background.y = display.contentCenterY
 
local platform = display.newImageRect( "platform.png", 300, 50 )
platform.x = display.contentCenterX
platform.y = display.contentHeight-25
```

As you probably noticed, there is one minor change compared to the background: instead of positioning the platform in the vertical center, we want it near the bottom of the screen. By using the command display.contentHeight, we know the height of the content area. But remember that platform.y places the center of the object at the specified location. So, because the height of this object is 50 pixels, we subtract 25 pixels from the value, ensuring that the entire platform can be seen on screen.

Save your main.lua file and relaunch the Simulator to see the platform graphic.

## Loading the Balloon

To load the balloon, we'll follow the same process. Below the previous commands, type these lines:

```lua
local balloon = display.newImageRect( "balloon.png", 112, 112 )
balloon.x = display.contentCenterX
balloon.y = display.contentCenterY
```

In addition, to give the balloon a slightly transparent appearance, we'll reduce the object's opacity (alpha) slightly. On the next line, set the balloon's alpha property to 80% (0.8):

```lua
local balloon = display.newImageRect( "balloon.png", 112, 112 )
balloon.x = display.contentCenterX
balloon.y = display.contentCenterY
balloon.alpha = 0.8
```

Save your main.lua file and relaunch the Simulator. There should now be a balloon in the center of the screen.

## Adding Physics

Time to get into physics! Box2D is the included physics engine for your use in building apps and games. While using physics is not required to make a game, it makes it much easier to handle many game situations.

Including physics is very easy. Below the previous lines, add these commands:

```lua

local physics = require( "physics" )
physics.start()
```

Let's explain these two lines in a little more detail:

The command local physics = require( "physics" ) loads the Box2D physics engine into your app and associates it with the local variable physics for later reference. This gives you the ability to call other commands within the physics library using the physics namespace variable, as you'll see in a moment.

physics.start() does exactly what you might guess — it starts the physics engine.

If you save and relaunch you won't see any difference in your game... yet. That is because we haven't given the physics engine anything to do. For physics to work, we need to convert the images/objects that were created into physical objects. This is done with the command physics.addBody:

```lua
local physics = require( "physics" )
physics.start()
 
physics.addBody( platform, "static" )
```

This tells the physics engine to add a physical "body" to the image that is stored in platform. In addition, the second parameter tells Solar2D to treat it as a static physical object. What does this mean? Basically, static physical objects are not affected by gravity or other physical forces, so anytime you have an object which shouldn't move, set its type to "static".

Now add a physical body to the balloon:

```lua
local physics = require( "physics" )
physics.start()
 
physics.addBody( platform, "static" )
physics.addBody( balloon, "dynamic", { radius=50, bounce=0.3 } )
```

In contrast to the platform, the balloon is a dynamic physical object. This means that it's affected by gravity, that it will respond physically to collisions with other physical objects, etc. In this case, the second parameter ("dynamic") is actually optional because the default body type is already dynamic, but we include it here to help with the learning process.

The final part of this physics.addBody command is used to adjust the balloon's body properties — in this case we'll give it a round shape and adjust its bounce/restitution value. Parameters must be placed in curly brackets ({}) (referred to as a table in the Lua programming language).

Because the balloon is a round object, we assign it a radius property with a value of 50. This value basically matches the size of our balloon image, but you may need to adjust it slightly if you created your own balloon image.

The bounce value can be any non-negative decimal or integer value. A value of 0 means that the balloon has no bounce, while a value of 1 will make it bounce back with 100% of its collision energy. A value of 0.3, as seen above, will make it bounce back with 30% of its energy.

### Notes

A bounce value greater than 1 will make an object bounce back with more than 100% of its collision energy. Be careful if you set values above 1 since the object may quickly gain momentum beyond what is typical or expected.

Even if you change the balloon's bounce property to 0, it will still bounce off the platform object because, by default, objects have a bounce value of 0.2. To completely remove bouncing in this game, set both the balloon and the platform to bounce=0.

Save your main.lua file and relaunch the Simulator. As a fun experiment, you can try adjusting the bounce value and relaunch the project to see the effect.