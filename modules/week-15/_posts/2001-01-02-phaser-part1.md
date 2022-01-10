---
title: Phaser.io Part 1
module: 14
jotted: true
---

# Phaser.io Part 1

<iframe width="560" height="315" src="https://www.youtube.com/embed/8Yz4Q_amBYI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

This first part is just setting up the canvas. Even though you may have not seen this libary before, the concepts will look the same.  Let's look at the first step.  Create a file called: part1.html and paste this code into it:

```html
<!doctype html> 
<html lang="en"> 
<head> 
    <meta charset="UTF-8" />
    <title>Making your first Phaser 3 Game - Part 1</title>
    <script src="//cdn.jsdelivr.net/npm/phaser@3.11.0/dist/phaser.js"></script>
    <style type="text/css">
        body {
            margin: 0;
        }
    </style>
</head>
<body>

<script type="text/javascript">

    var config = {
        type: Phaser.AUTO,
        width: 800,
        height: 600,
        scene: {
            preload: preload,
            create: create,
            update: update
        }
    };

    var game = new Phaser.Game(config);

    function preload ()
    {
    }

    function create ()
    {
    }

    function update ()
    {
    }

</script>

</body>
</html>
```

You will see that it is setting up the parameters of the Phaser class. It is essentially creating a new canvas. Notice the three functions as well.  Preload, Create and Update.  These are the three essential functions.  The `preload` will load all the assets at the page is loading, the it will set up the page using the `create` and then finally, the `update` function will get called repeatedly in any game.  Run this with the Live Server.  Did you get a black screen?  Good job! :)