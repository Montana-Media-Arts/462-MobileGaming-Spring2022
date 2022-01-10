---
title: Classes and Objects Example
module: 7
jotted: true
---

# An Example using Classes and Objects

Let's finish out the Person class example so that you can see all of this in use.

## Define a Class

First, we need to write our class. We know we want this class to be a digital representation of a "person", so let's label it as such.  Our class initially looks like the following;

```js
class Person {
    constructor() {

    }
}
```

## Consider Object Properties

So, we should also consider what a person can do.  That is what we did in the previous section. They could walk and get the timeToTravel.

For our example, let's have our main properties eyeColor and hairColor, and then the methods or functions be walk and timeToTravel.

- eye color that is brown
- hair color that is blonde

The Person will also:

- walk
- get the time to travel a certain distance

These specifications can help us determine the properties the Person will need. We can say that the Person will likely need;

- an eye color property
- a hair color property
- a walking speed property
- a distance property

Below is the following constructor method.

```js
class Person {
    constructor( eyeColor, hairColor, speed, distance ) {
        this.eyeColor = eyeColor;
        this.hairColor = hairColor;
        this.speed = speed;
        this.distance = distance;
    }
}
```

## Consider Object Methods

The next step might be to start writing the methods objects of this class may need. Since we are trying to write modular, highly-readable code, we want to try and write methods that do individual, well-defined tasks. With that in mind, we can think about what people can do.

- Want to see the properties of the Person.
- A walking method
- A time to travel method.

With this in mind, let's write three methods.

#### toString

The first of these we may want to write is the method to display the parameters of the Person. toString is the most common method in any language.  You can find this method in most Object-Oriented programming languages.

In this method, we need to access the Person's eyeColor, hairColor, speed, and distance properties and returned as a string.

```js
toString() {
    let str;
    str = `This person has ${this.eyeColor} eyes, has ${this.hairColor} hair, and is currently moving at ${this.speed} miles per hour.`;
    return str;
}
```
<br/>
<iframe width="560" height="315" src="https://www.youtube.com/embed/ZsP8v5D1ur4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

#### Person walking

To walk, the Person will need a walking method.

```js
walk() {
    return `I am walking across the tundra at ${this.speed} miles per hour`;
}
```

#### Time to travel method

We may also want to know how long it takes them to travel a certain distance, so we would have a timeToTravel method to calculate this.

```js
timeToTravel()
{
    let time = this.distance/this.speed;
    return time;
}
```
<br/>
<iframe width="560" height="315" src="https://www.youtube.com/embed/G8zPtAv139U" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


#### Getters and Setters

Remember when we were talking about changing the values of our properties directly and how that wasn't the best idea?  We want to use getters and setters -- these are special methods -- to make those changes for us.  It helps keep better control over who and when properties are changed. This technique is called **encapsulation**.  It just means we want the class to make changes to our properties, not the outside world.  So, we give access through getters and setters.

An example would be something like this:

```js
    get eColor() {
        return this.eyeColor;
    }
    set eColor(eyeColor) {
        this.eyeColor = eyeColor;
    }
```
<br/>
<iframe width="560" height="315" src="https://www.youtube.com/embed/jxKCJP51Rl8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

#### Altogether

Altogether, the class definition might look like;


```js

class Person {
    constructor( eyeColor, hairColor, speed, distance ) {
        this.eyeColor = eyeColor;
        this.hairColor = hairColor;
        this.speed = speed;
        this.distance = distance;
    }
    get eColor() {
        return this.eyeColor;
            }
    set eColor(eyeColor) {
        this.eyeColor = eyeColor;
    }
   walk() {
        return `I am walking across the frozen tundra at ${this.speed} miles per hour`;
    }
    timeToTravel()
    {
        let time = this.distance/this.speed;
        return time;
    }
    toString() {
        let str;
        str = `This person has ${this.eyeColor} eyes, has ${this.hairColor} hair, and is currently moving at ${this.speed} miles per hour.`;
        return str;
    }
}
```

# Creating and Using a Person Object

To create and use a Person object in JS, we will need to;

- create a variable to store a reference to the object in
- create a new object and store it in the variable
- call the object's methods


#### Create a Variable

First, created a variable for which to store a reference to the object.

```js
let myPerson;
```

#### Create a new Person Object

Next, we will create a new Person object and then bind this object to `myPerson`. Also, we have four parameters that we need to pass to the Person's constructor function. Again these are; `eyeColor`, `hairColor`, `speed`, and `distance`.

```js
myPerson = new Person( 'blue', 'brown',3,10);
```

#### Call the Person's Methods

Finally, we can use our Person object.


Look how clean and straightforward that code below looks! It is so easy to read and understand. By abstracting the Person into a class, we can create a person object that we can call the methods from each of those objects. Each one makes sense and is readable!

```html
<html>
<head>
    <title>OOP</title>
    <script>
        class Person {
        constructor( eyeColor, hairColor, speed, distance ) {
            this.eyeColor = eyeColor;
            this.hairColor = hairColor;
            this.speed = speed;
            this.distance = distance;
        }
            get eColor() {
                return this.eyeColor;
            }
            set eColor(eyeColor) {
                this.eyeColor = eyeColor;
            }
            walk() {
                return 'I am walking across the frozen tundra at ' + this.speed + ' miles per hour';
            }
            timeToTravel()
            {
                let time = this.distance/this.speed;
                return "It will take approximately " + 
                Math.round(time) + " hours to cover " + this.distance + " miles.";
            }
            toString() {
                let str;
                str = 'This person has ' + 
                this.eyeColor + ' eyes, has '
                + this.hairColor +
                ' hair, and is currently moving at ' + 
                this.speed + ' miles per hour.';
                return str;
            }
        }

        function createAndShow()
        {
            let myPerson = new Person( 'blue', 'brown',3,10);
            document.getElementById("myWalk").innerHTML = myPerson.walk();
            document.getElementById("myTimeToTravel").innerHTML = myPerson.timeToTravel();
            document.getElementById("myPerson").innerHTML = myPerson.toString();    
        }
    </script>
</head>
<body>
    <div id="myWalk"></div>
    <div id="myTimeToTravel"></div>
    <div id="myPerson"></div>
    <script>
        createAndShow();   
    </script>
</body>
</html>
```
<br/>
<iframe width="560" height="315" src="https://www.youtube.com/embed/hf-z7przdp0" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>