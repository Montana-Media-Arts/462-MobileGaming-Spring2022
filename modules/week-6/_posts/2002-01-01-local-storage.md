---
title: Local Storage
module: 6
jotted: false
---

# Local Storage

So, what is **local storage**? You have used the query string and cookies, but what other mechanisms are there for storing information?  One is local storage.  It allows us to store information on a client without having to have a domain (like a cookie does), and you don't have to worry about having data in the query string in cleartext.

So, how does it work?  Here is the syntax of the two files required:

```html
<html>
    <head>
        <title>
            JSON FTW
        </title>
        <script>
            function getInformation()
            {
                var information = {"car": "dodge", "year":"2016", "color":"blue"};
                document.getElementById("info").innerHTML = information.car + ":" + information.year + ":" + information.color;
                localStorage.setItem("information", JSON.stringify(information));
            }
            
            function goNextPage()
            {
                window.location = "Page2.html";
            }
        </script>
    </head>
    <body onload="getInformation();">
        <div id="info"></div>
        <br>
        <button id="btnSubmit" onclick="goNextPage();">Go to Next Page</button>
    </body>
</html>
```

Whereas Page 2 looks like this:


```html
<html>
    <head>
        <title>
            JSON FTW
        </title>
        <script>
            function getInformation()
            {
                var information = localStorage.getItem("information");
                document.getElementById("info").innerHTML = "<h1>" + JSON.parse(information).car + "</h1>";
            }
            
            function goNextPage()
            {
                window.location = "Page1.html";
            }
        </script>
    </head>
    <body onload="getInformation();">
        <div id="info"></div>
        <br>
        <button id="btnSubmit" onclick="goNextPage();">Go to Next Page</button>
    </body>
</html>
```

You may notice that I needed first to change the JSON object to a string before I stored it in local storage.  Then, when I got it out of local storage since it's formatted correctly, I parsed it back into a JSON object.

Again, the **stringify** and **parse** functions come from the JSON class.  Cool huh?

<iframe width="560" height="315" src="https://www.youtube.com/embed/X-3_05yBklQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>