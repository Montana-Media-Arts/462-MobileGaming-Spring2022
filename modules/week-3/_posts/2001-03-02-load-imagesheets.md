---
title: Load Image Sheets
module: 3
jotted: true
---

# Load Image Sheets

If you've used another game development platform, you may be familiar with the term "sprite sheet" or "texture atlas." In Solar2D, it is called an image sheet and it allows you to load multiple images/frames from a single larger image file. Image sheets are also used for animated sprites, where frames for the sprite are pulled from the sheet and assembled into an animated sequence.

### Note
Image sheets are most easily created using a tool such as TexturePacker which collects, organizes, and packs multiple images into a compatible image sheet. While this software isn't a requirement, it does save you time and energy.

Following your existing code, create a sheetOptions table as shown below. Note that it should contain a child table, frames, which will contain an array of Lua tables defining each frame in the sheet.

```lua
-- Seed the random number generator
math.randomseed( os.time() )
 
-- Configure image sheet
local sheetOptions =
{
    frames =
    {
 
    },
}
```

When configuring an image sheet, you must specify where the images are located within the sheet. For this game, every image is different in size, so we must provide four specific properties which define the theoretical "bounding box" for the portion of the image sheet to utilize:

* x — the upper-left corner point of the image in x coordinates, relative to the overall sheet width.
* y — the upper-left corner point of the image in y coordinates, relative to the overall sheet height.
* width — the total width of the image.
* height — the total height of the image.

With this concept in mind, add five Lua tables inside the frames table to declare the position and size of each image within the sheet:

```lua
-- Configure image sheet
local sheetOptions =
{
    frames =
    {
        {   -- 1) asteroid 1
            x = 0,
            y = 0,
            width = 102,
            height = 85
        },
        {   -- 2) asteroid 2
            x = 0,
            y = 85,
            width = 90,
            height = 83
        },
        {   -- 3) asteroid 3
            x = 0,
            y = 168,
            width = 100,
            height = 97
        },
        {   -- 4) ship
            x = 0,
            y = 265,
            width = 98,
            height = 79
        },
        {   -- 5) laser
            x = 98,
            y = 265,
            width = 14,
            height = 40
        },
    },
}
```

The order in which you declare each image within a sheet is very important — later, when you load an image from a sheet using a command such as display.newImageRect(), you'll need to specify the number of the frame based on the order in which it was declared in the sheet configuration.

With this table of information, we can now load the image sheet into memory with the graphics.newImageSheet() command. This accepts the name of the image file for the image sheet (gameObjects.png) and a reference to the sheetOptions table which we just created:

```lua

    },
}
local objectSheet = graphics.newImageSheet( "gameObjects.png", sheetOptions )
```