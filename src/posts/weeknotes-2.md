---
layout: layouts/post.njk
title: "Weeknotes #2"
date: 2020-04-21T17:42:27.373Z
tags:
  - blog
---
Following the unexpected bonus of getting to build an app front end in collaboration with [Jayme Waye](https://github.com/jaymew88) last week, it was time to go back to school with the first week of Sprint 6 of the Practicum By Yandex Web Developer track. 

Week 1 of a Sprint is a series of lessons, 55 of them in total this week, designed to prepare us for the project that we'll have to deliver by the end of week 2. I don't know how anybody else feels about them, but I have a tendency to rush through them as quickly as possible in order to "get to the good stuff" and, 9 times out of 10, I end up having to go back to re-read stuff 🤷‍♂️.

# Sprint 6: Week 1

I can't tell you how much I learned in this week's lessons - I had my mind blown several times 🤯. I could rehash some of the lessons here but I think that the best way for me to show what I learned is by showing you how I implemented it in a project.

In Sprint 4 we designed a single page website that allowed you to change the name and job description of the on-screen profile via a modal popup form. I can't tell you how happy I was when I got this working - it felt like a 🧙.

![A gif showing the edit](https://www.dropbox.com/s/4b0dkqd13l4ov2u/ezgif.com-optimize.gif?raw=1)
Having said that, this project obviously needed a lot more work and I made a note saying as much in the README file in the [repo](https://github.com/jimiryquai/around_the_us).

What's that saying? Be careful what you wish for? Here's what we've been asked to do by the end of the sprint:

1. When the page is loaded, there must be six cards. Use JavaScript to add them.
2. Add a form for adding a new card to your project.
3. Develop a feature that will let users add custom cards.
4. Code the "Like" button for the cards.
5. Add a delete icon to the cards. Then, make your buttons work by writing the needed code.
6. When a user clicks on a picture, the popup with that picture should open. When they click "Close," it should close.
7. Make the popup opening and closing look smooth. When being opened, all the popups should smoothly appear out from transparency, and when being closed, they should smoothly become completely transparent again.

So the first item in the list was obviously the most pressing concern as we were being asked to turn our hard-coded HTML into dynamically rendered JavaScript. Shots fired 🔫!

To be fair to the guys at Practicum by Yandex, they gave us a massive clue, and head start, bu providing us with an array of objects containing the names and urls of the locations and their images. It looked something like this:


