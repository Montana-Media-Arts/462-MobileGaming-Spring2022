---
title: Types & Values
module: 3
jotted: true
---

# Values, Data Types, & Operators



Please read the following;

- Haverbeke, Marijn. **Eloquent JavaScript: A Modern Introduction to Programming.** 3rd Edition. N.p., 2018. Web.
    - [_Chapter 1; Values, Types, and Operators_](http://eloquentjavascript.net/3rd_edition/01_values.html)
- **JavaScript Guide.** MDN web docs. 2018. Web.
    - [_Grammar and Types_](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_Types)
    - [_Expressions and operators_](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Expressions_and_Operators)



## Goals

At the end of the chapter you should have an understanding for;

- **Values**
    - Regular Values
    - Empty Values
        - `null`
        - `undefined`
- **Data Types**
    - Numbers
        - Regular Numbers
        - Special Numbers
    - Strings
        - regular strings (`"Hello World!"`, `'single quote string'`)
        - special characters (i.e., `\n`, `\t`)
        - template literal strings (``these use backticks and have special properties``)
    - Booleans

**Video**
<div class="embed-responsive embed-responsive-16by9"><iframe width="560" height="315" src="https://www.youtube.com/embed/XSI_ta0mvOE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>

- **Operators**
    - Basic mathematical operators
        - addition/subtraction on numbers (`+`/`-`)
        - multiplication/division on numbers (`*`/`/`)
        - the modulo on numbers (`%`)
    
**Video**
<div class="embed-responsive embed-responsive-16by9"><iframe width="560" height="315" src="https://www.youtube.com/embed/isrkyyJfAz4" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>

    - String operators
        - String concatenation (`+`)
    
**Video**
<div class="embed-responsive embed-responsive-16by9"><iframe width="560" height="315" src="https://www.youtube.com/embed/DTk3ptbINGo" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>

    - Unary Operators
        - `typeof`

    
**Video**
<div class="embed-responsive embed-responsive-16by9"><iframe width="560" height="315" src="https://www.youtube.com/embed/O6_MphRS0E8" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>

    - Comparison Operators
        - `<`, `>`,`<=`, `>=`, `==`, `!=`
    - Logical Operators
        - or - `||`
        - and - `&&`
        - not - `!`
    - Type Conversion
    
**Video**
<div class="embed-responsive embed-responsive-16by9"><iframe width="560" height="315" src="https://www.youtube.com/embed/yjg6D7B7ozM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></div>


## Interactive JS Console

While you work on this chapter, you should use the following interactive JS console to test out values, types, and operators.

<div id="jotted-demo-1" class="jotted-theme-stacked"></div>

<script>
    new Jotted(document.querySelector("#jotted-demo-1"), {
    files: [
        {
            type: "js",
            hide: false,
            content: "// try out operators, values, etc, here...\n\n// as an example\nconsole.log( typeof \"Hello World!\");\nconsole.log( 5*10 == 50 );\n\n\n"
        }
    ],
    showBlank: false,
    showResult: false,
    plugins: [
        { name: 'ace', options: { "maxLines": 50 } },
        { name: 'console', options: { autoClear: false } },
    ]
});
</script>