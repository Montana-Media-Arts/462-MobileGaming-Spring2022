---
title: Learning jQuery
module: 8
jotted: false
---

# Learning jQuery

Previously, we looked at the basics of accessing items through the DOM. What other functions are available to us?  We looked at toggle.  Below are even more methods.

Methods:

1. fadeIn()
2. fadeOut()
3. fadeToggle()
4. fadeTo()
5. slideDown()
6. slideUp()
7. slideToggle()
8. animate()

So, how do they function?

Here is an example:

```html
<!DOCTYPE html>
<html>

<head>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
    <script>
        $(function () {


        });
        $(document).ready(function () {
            $("button").click(function () {
                $(".myGreatClass").fadeOut();
            });
        });
    </script>
</head>

<body>

    <p id="infoid">This is a paragraph.</p>
    <p class="myGreatClass" style="background-color:red">This is the second paragraph.</p>
    <button>Click me to hide paragraphs</button>
    <br>
</body>

</html>
```
<br/>
<iframe width="560" height="315" src="https://www.youtube.com/embed/uO4Qxymj26w" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Now, try some of these other methods and see what happens.  Just replace fadeOut with the name of the function you want to try.

What about animate?  It is a little different than the other methods listed above.  Let's look at it closer.

```html
<!DOCTYPE html>
<html>

<head>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
    <script>
        $(function () {


        });
        $(document).ready(function () {
            $("button").click(function () {
                $(".myGreatClass").animate({left: '250px'});
            });
        });
    </script>
</head>

<body>

    <p id="infoid">This is a paragraph.</p>
    <p class="myGreatClass" style="background-color:red;position:absolute; top: 100px; left: 25px">This is the second paragraph.</p>
    <button>Click me to hide paragraphs</button>
    <br>
</body>

</html>
```

Again, we are just updating the style of this particular tag, but in a cooler way by adjusting its left property.

<iframe width="560" height="315" src="https://www.youtube.com/embed/72rOPWTTiYA" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>