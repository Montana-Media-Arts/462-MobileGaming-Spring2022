---
title: Load Background
module: 3
jotted: true
---

# Load Background

As in the previous project, we'll load the background image first:

```lua

-- Load the background
local backGroup = display.newGroup()

local background = display.newImageRect("background.png", 800, 1400 )
background.x = display.contentCenterX
background.y = display.contentCenterY

backGroup:insert(background)
```

These commands should appear straightforward at this point, but there is one very important difference! Inspect the first parameter to display.newImageRect() — before the image file name (now the second parameter), we indicate the display group (backGroup) in which to place the object. This is a convenient inline shortcut to specify the display group to insert the background image once it's loaded.