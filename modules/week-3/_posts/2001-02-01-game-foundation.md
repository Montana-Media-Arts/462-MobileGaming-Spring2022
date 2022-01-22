---
title: Game Foundation
module: 3
jotted: true
---

# Game Foundation

Now that you understand basic settings and configuration, let's continue with creating the game.

## Physics Setup

Like the BalloonTap project, this game will use the physics engine, so let's configure it right from the beginning. If you're using physics, it's often best to include your basic physics setup code early in the program.

Using your chosen text editor, open the main.lua file within your project folder and type these commands:

```lua

local physics = require( "physics" )
physics.start()
physics.setGravity( 0, 0 )
```

As you can see, after loading and starting the physics engine, we set gravity values. By default, the physics engine simulates standard Earth gravity which causes objects to fall toward the bottom of the screen. To change this, we use the physics.setGravity() command which can simulate gravity in both the horizontal (x) or vertical (y) directions. Since this game takes place in outer space, we are going to assume that gravity does not apply. Thus, we set both values to 0.

## Random Seed

Our game will randomly spawn asteroids outside of the screen edges, so we'll be implementing random number generation further along in this project. First, though, we need to set the "seed" for the pseudo-random number generator. On some operating systems, this generator begins with the same initial value which causes random numbers to repeat in a predictable pattern. The following addition to our code ensures that the generator always starts with a different seed.

```lua

local physics = require( "physics" )
physics.start()
physics.setGravity( 0, 0 )

-- Seed the random number generator
math.randomseed( os.time() )
```

On the first of these two lines, observe the double minus signs (--). These are used to tell Lua that it should ignore everything else on the line. This is so that you can leave yourself comments (notes) in the code. While it might not seem important when you are initially writing the program, the more complex the app gets, or the more time that goes by before you return to work on the app again, the more important it is to include comments for reference.

When you intend to generate random numbers in an app, seed the pseudo-random number generator just once, typically within main.lua. Doing so multiple times is redundant and unnecessary.

## Including Images

Initially we'll need just two visual assets for this project. As before, they should be placed within your StarExplorer project folder.
[image download](https://github.com/coronalabs/GettingStarted02/archive/master.zip)

