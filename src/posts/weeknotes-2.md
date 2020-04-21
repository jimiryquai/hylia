---
layout: layouts/post.njk
title: "Weeknotes #2"
date: 2020-04-21T17:42:27.373Z
tags:
  - blog
---
Following the unexpected bonus of building an app in collaboration with [Jayme Waye](https://github.com/jaymew88), last week it was time to go back to school with the first week of Sprint 6 of the Practicum By Yandex Web Developer track. Week 1 of a sprint is a series of lessons designed to prepare us for the project that we'll have to deliver by the end of week 2. I don't know how anybody else feels about them but I have a tendency to rush through them as quickly as possible in order to "get to the good stuff" and 9 times out of 10 I end up having to go back to re-read stuff 🤷‍♂️.

# Sprint 6: Week 1

### Intro to Primitives, Conditions, and Loops

There were 19 lessons inside this module and a lot of the lessons were like refresher lessons to me as I had studied the material before. It wasn't long until I had a 💡 moment though!

**Lesson 3.** Primitive Data Types and the `typeof` Operator

### Checking data types with the `typeof` operator

So what did I learn here? A few things actually...

1. The `typeof` operator returns a string:

   ```javascript
   typeof 10; // "number"
   typeof "Hello World!"; // "string"
   typeof true; // "boolean"
   typeof undefined; // "undefined"
   ```
2. The data we check with `typeof` is called an operand and if you need to know the type of an entire expression then you need to wrap it in parentheses or something weird happens:

   ```javascript
   typeof (10 + 5) // "number"
   typeof 10 + 5 // "number5"

   /* in the second case, the operator 
   checked the type of 10, and then concatenated 
   the result with 5 to give us "number5" */
   ```

   At first, the second case ☝️ blew my mind 🤯. I was expecting it to return "number""number" but when I thought about it more deeply I realised that the lack of brackets meant that the type of 10 had been checked and the string "number" had been returned. Then, because we tried to add a different data type (a number) to this string, implicit conversion to string occurred and the end result was (Mambo?) "number5".
3.