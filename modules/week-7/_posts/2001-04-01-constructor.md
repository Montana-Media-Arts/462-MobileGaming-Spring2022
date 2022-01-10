---
title: Constructor Method
module: 7
jotted: false
---

# Class Constructor Methods

In every class definition written, there should be at least one method; that is the `constructor` method. Furthermore, typically this should be the first method defined. It doesn't have to be, but by convention and for readability, it is usually the first thing in the class.

The constructor method **is always** called by JavaScript when creating a new object from a class. Therefore, you **must** have a constructor method.  What is the constructor, you say?  Well, think of the word construct.  What does that mean?  It means to build or construct. So, what the constructor is doing is creating the object from the class.  Cool huh?

## The Purpose of the Constructor Method

JavaScript uses the **constructor** to build new objects of a class type. You have created an object before -- think about creating a new Array().  Those parentheses at the end of the Array is calling the constructor.  Come on, that's cool, right?

#### So what goes in a _constructor method_?

The constructor method _initializes_ an object's _properties_.

As an example, if we were creating a Person, we may want to specify properties such as:

- `eyeColor`
- `numberOfLegs`
- `numberOfArms`
- `hairColor`

You will learn more specifically how to do this on the next page.

## Constructor Example

As mentioned, the _constructor method_ should be the first method in a _class definition_.

Furthermore, if there is data that needed within the newly created object, this should be represented as _input parameters_ to this function, which works just like any other function.  You have done all of this before.  Don't you love it when it all comes full circle!

So our example might look like:

```js
// a class definition
class Person {

    // constructor method
    constructor( eyeColor, numberOfLegs, numberOfArms, hairColor ) {
        // method function block
        // Do stuff here to create an object
        console.log(eyeColor);
    }
}
```
<br/>
<iframe width="560" height="315" src="https://www.youtube.com/embed/p4xykn8VZUI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
