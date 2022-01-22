---
title: Settings and Configuration
module: 3
jotted: true
---

## Settings

In addition to main.lua, there are two important files which configure your app to work correctly on multiple types of devices: build.settings and config.lua.

### Build Settings
The build.settings file provides real devices (phones, tablets, etc.) with details they need regarding your app. This includes the supported orientations for the app, names of icon files, plugins to include, special information required by devices, and more.

Using your text editor, locate and open the build.settings file within your project folder. It will contain a lot of information, but let's focus on the highlighted block of code:

```lua

settings =
{
    orientation =
    {
        -- Supported values for orientation:
        -- portrait, portraitUpsideDown, landscapeLeft, landscapeRight
 
        default = "portrait",
        supported = { "portrait", },
    },
```

Our StarExplorer app will only be available to play in portrait mode, so we set this on the following two lines:

default = "portrait", — This line specifies that the game should begin in portrait orientation when the user first loads the app.

supported = { "portrait", }, — This line specifies that the only supported orientation is also portrait. That means that even if the user turns (orients) the physical device around in their hands, your app will remain locked in portrait orientation.

As you learned in the previous chapter, curly brackets indicate a table in the Lua programming language, and tables can contain multiple items. We could include up to four supported orientations inside this table, but since this app will support just one orientation, "portrait" is all that we need to include.

There are several additional things which can be included inside the build.settings file, but in the interest of keeping this guide as straightforward as possible, let's move on.

## Configuration Options

The config.lua file contains app configuration settings. This is where we specify what content resolution the app will run at, the content scale mode, how high-resolution devices should be handled, etc.

Using your text editor, locate and open the config.lua file within your project folder and inspect the following highlighted lines:

```lua

application =
{
    content =
    {
        width = 768,
        height = 1024, 
        scale = "letterbox",
```

Notice that this content table contains a series of configuration settings, including:

width and height — These values specify the content area size for the app. Your base content area can be whatever you wish, but often it's based around a common screen width/height aspect ratio like 3:4, set here by 768 and 1024.
It's important to understand that these values do not indicate an exact number of pixels, but rather a relative number of content "units" for the app. The content area will be scaled to fit any device's screen, with subtle differences dictated by the scale definition (see the next point).

scale — This important setting specifies how to handle the content area for screens which do not match the aspect ratio defined by the width and height settings, for example 3:4 in this case. The two most common options are "letterbox" and "zoomEven".
"letterbox" scales the content area to fill the screen while preserving the same aspect ratio. The entire content area will reside on the screen, but this might result in "black bars" on devices with aspect ratios that differ from your content aspect ratio. Note, however, that you can still utilize this "blank" area and fill it with visual elements by positioning them or extending them outside the content area bounds. Essentially, "letterbox" is an ideal scale mode if you want to ensure that everything in your content area appears within the screen bounds on all devices.

"zoomEven" scales the content area to fill the screen while preserving the same aspect ratio. Some content may "bleed" off the screen edges on devices with aspect ratios that differ from your content aspect ratio. Basically, "zoomEven" is a good option to ensure that the entire screen is filled by the content area on all devices (and content clipping near the outer edges is acceptable).

	
For this game, let's use "zoomEven" scale mode. Change scale = "letterbox", to the following and remember to save your config.lua file afterward!

```lua

application =
{
    content =
    {
        width = 768,
        height = 1024, 
        scale = "zoomEven",

```