---
layout: post
title:  "Understanding types in javascript"
date:   2023-08-22 10:18:00
comments: true
desc: "Javascript data types primitive and non-primitive"
keywords: js, javascript, types
category: js
---

Javascript has dynamic type - what that means is you don't have to define the type of a variable when you are declaring it, unlike other typed languages such as Golang.

Let's understand different types in javascript 
- `primitive`
- `non-primitive`

## Primitive Types 
In the simplest terms, these are types that are not objects or collections. There are 6 types of primitives:

- `undefined`: Represents a lack of existence. It's usually not defined explicitly, as doing so would defeat its purpose.
- `null`: Also represents a lack of existence. We define it to distinguish it from "undefined".
- `boolean`: Represents a true or false value.
- `number`: Encompasses all numeric types like integers, floating-point numbers, etc.
- `string`: Represents a sequence of characters.
- `symbol`: This is a relatively new type introduced in ES6. It's not supported by all browsers.

## Non-Primitive Types

- `object`


## Notes
In case of primitive types - if defined variable `a` and have memory `0x001`. when you assign `b = a` it creates new memory 

non-primitive types - it uses same memory. however if used `=` operator with new value it sets up new memory.