---
title: Variables again
module: 4
---

# Variables again <br />


<br />

You might be asking yourself, why are we covering variables again?  Well, they are the cornerstone of programming, so it's good to have a solid grasp on them.

What does that mean to us?

Remember from last week, that we can declare a variable like this:

- var
- let
- const

Now, do you remember what those all mean?

If I were to ask you to create a program that gets a user's name and then put it into a variable, do you think you could that? 

If not, that's okay!  I will show you how.

First, create a file called GetName.html.

Then, add a textbox into that file.

```html
<html>
    <body>
        <label id="lblName">Your Name Goes Here</label><br>
        <input id="txtName" type="text"><br>
        <button id="btnSubmit">Submit</button><br>
    </body>
</html>
```

Now, open the file in your favorite browser (still hopefully Chrome).  Does it show a textbox and a button? Great!

Now, we need to get the information out of the text box.  How are we going to do that?  Well, first, then we need to do is get the text from the label.

We need to add some JavaScript to access the DOM (quick check, you remember the DOM right?  If not, it stands for Document Object Model)

```html
<html>
    <body>
        <label id="lblName">Your Name Goes Here</label><br>
        <input id="txtName" type="text"><br>
        <button id="btnSubmit">Submit</button><br>

         <script>
            var currentText = document.getElementById("lblName").innerHTML;
            // we can either use console.log(currentText); 
            // to see what is stored in the tag it will show in the console
            // we can use window.alert(currentText); 
            // to see what is stored in that tag
        </script>
    </body>
</html>
```


<iframe width="560" height="315" src="https://www.youtube.com/embed/g2SFQfttRYg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
