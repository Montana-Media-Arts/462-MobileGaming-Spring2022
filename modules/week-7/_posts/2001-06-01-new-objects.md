---
title: Creating new Objects from Classes
module: 7
jotted: false
---

# Creating Objects from Classes

A lot of discussions have occurred about classes and objects, yet you still do not know how to create an object from your class definition formally!

To create a new object "of class type _X_", you need to call the `new` keyword, followed by the name of the class, including any constructor input parameters within parentheses trailing the class name.  Remember, we did this with the Array class.  It had the parentheses, but no parameters.

The following creates a new object of class type `Person`, and passes it two input parameters. The variable `myPerson` stores the new object.

```js
let eyeColor = "blue";
let hairColor = "green";
let myPerson = new Person( eyeColor, hairColor );
```
<br/>
<iframe width="560" height="315" src="https://www.youtube.com/embed/gGc6NUT1Mnc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


# Accessing an Objects Properties

To access the properties of an object, we will use the same "_dot notation_" as we learned about with objects' data structures.

```js
myPerson.eyeColor; // ← returns the value of 'myPerson's eyeColor.
```

We can also set object properties using this same notation.

```js
myPerson.hairColor = "purple"; // ← sets the value of the property to purple
```

**NOTE:** Typically, when using classes and OOP paradigms, setting object properties with this notation is considered poor style. Direct access can lead to errors in code, and we will discuss this later.

<iframe width="560" height="315" src="https://www.youtube.com/embed/r4mjFdaet5E" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# Calling Object Methods

Object methods use the _dot notation_.   Parenthesis is always added to the method name, regardless of whether input parameters are being passed into the method.

```js
myPerson.walk(); // ← executes myPerson's method, 'walk'.

myPerson.timeToTravel(distance); // ← execute the method and pass it one input parameter value.
```
<br/>
<iframe width="560" height="315" src="https://www.youtube.com/embed/q_wACy_hEGI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>