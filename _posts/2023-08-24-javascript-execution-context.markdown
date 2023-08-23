---
layout: post
title:  "Javascript Fundamentals - Execution Context"
date:   2023-08-24
comments: true
desc: "Javascript Fundamentals - Execution Context"
keywords: js, javascript, execution, context
category: js
---

> Everything happens in javascript happens inside Execution Context

Is javascript really asynchronous? do you know?

Before understanding nuances of EC (Execution Context) there are some pre-requisites

<b>Syntax Parser</b> - checks the syntax and reads line by line as per the specifications. Read more [here](https://medium.com/r?url=https%3A%2F%2Fjavascript.plainenglish.io%2Funderstanding-javascript-parsers-in-2020-a2f00830d5fe)

<b>JS Engine</b> - converts source code to machine code for CPU to understand, developed by browsers. Read more [here](https://www.geeksforgeeks.org/introduction-to-javascript-engines/)

### How it all starts
When browser reading through HTML and when it encounters any form of javascript be it `<script>` tags or as part of attribute having js method, it sends to JS engine, which eventually creates an envrironment to handle transformation and execution of code. This environment is call Execution Context.

<b>What happens when EC is created:</b>
It parse the code (Syntax Parser)
Variables/functions stored in memory

#### EC Types:

<b>Global</b> - created when a javascript script first starts to run and represent global scope

<b>Function</b> - created when function is called, representing the function's local scope

#### Phases of EC:
Creation (happens in 3 stages)
- Variable object/envrionment - stores all variables (all declared with `var` keyword stored with value `undefined`) and functions. This process of storing is called Hoisting - storing in memory and made available before execution of code[^1]
- Scope chain - reference of outer environment until global execution context is reached
- Setting value of this
Execution

Javascript is single thread and synchronous
Lets understand from an example: lets say we have below script to be executed.

```javascript
function x() {
    y();
    var p;
}
function y() {
    var q;
}
x();
var r;
```

It will create Global Execution Context
It will create function execution context for x
It will create function execution context for y
It will run `var q;` then terminate function context of y
It will run `var p;` then terminate function context of x
Run `var r;` and terminate global execution context

#### Summary:
As you see - all the steps are in sequence and happen one after other, even if there are other requests, they wait in event pool. Our beloved javascript indeed work synchronously and single thread.

### Footnotes:
[^1]: this means, irrespective of order you have defined function it will picked up first. So ideally you can call a function before its definition, opposed to other languages.
Doesn't work with keyword `let` or `const`
