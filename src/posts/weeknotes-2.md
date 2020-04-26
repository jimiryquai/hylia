---
layout: layouts/post.njk
title: "Weeknotes #2"
date: 2020-04-26T20:41:32.018Z
tags:
  - blog
  - javascript
---
Following the unexpected bonus of getting to build an app front end in collaboration with [Jayme Waye](https://github.com/jaymew88) last week, it was time to go back to school with the first week of Sprint 6 of the Practicum By Yandex Web Developer track. 

Week 1 of a Sprint is a series of lessons, 55 of them in total this week, designed to prepare us for the project that we'll have to deliver by the end of week 2. I don't know how anybody else feels about them, but I have a tendency to rush through them as quickly as possible in order to "get to the good stuff" and, 9 times out of 10, I end up having to go back to re-read stuff 🤷‍♂️.

# Sprint 6: Week 1

I can't tell you how much I learned in this week's lessons - I had my mind blown several times 🤯. I could rehash some of the lessons here but I think that the best way for me to show what I learned is by showing you how I implemented it in a project.

In Sprint 4 we designed a single page website that allowed you to change the name and job description of the on-screen profile via a modal popup form. I can't tell you how happy I was when I got this working - it felt like a 🧙.

![A gif showing the edit](https://www.dropbox.com/s/4b0dkqd13l4ov2u/ezgif.com-optimize.gif?raw=1) Having said that, this project obviously needed a lot more work and I made a note saying as much in the README file in the [repo](https://github.com/jimiryquai/around_the_us).

What's that saying? Be careful what you wish for? Here's what we've been asked to do by the end of the sprint:

1. When the page is loaded, there must be six cards. Use JavaScript to add them.
2. Add a form for adding a new card to your project.
3. Develop a feature that will let users add custom cards.
4. Code the "Like" button for the cards.
5. Add a delete icon to the cards. Then, make your buttons work by writing the needed code.
6. When a user clicks on a picture, the popup with that picture should open. When they click "Close," it should close.
7. Make the popup opening and closing look smooth. When being opened, all the popups should smoothly appear out from transparency, and when being closed, they should smoothly become completely transparent again.

So the first item in the list was obviously the most pressing concern as we were being asked to turn our hard-coded HTML into dynamically rendered JavaScript. Shots fired 🔫!

## When the page is loaded, there must be six cards. Use JavaScript to add them.

To be fair to the guys at Practicum by Yandex, they gave us a massive clue, and head start, by providing us with an array of objects containing the names and urls of the locations and their images. It looked something like this:

```javascript
const cards = [
    {
        name: "Yosemite Valley",
        link: "https://code.s3.yandex.net/web-code/yosemite.jpg"
    },
    {
        name: "Lake Louise",
        link: "https://code.s3.yandex.net/web-code/lake-louise.jpg"
    },
    {
        name: "Bald Mountains",
        link: "https://code.s3.yandex.net/web-code/bald-mountains.jpg"
    },
];
```

We'd just learned an awful lot about arrays, their methods, event listeners and HTML templates in the lessons leading up to this project so it was time for the rubber to hit the 🛣️ and put the theory into practice!

First up, I commented out the hard-coded HTML for the six cards in the photo-grid element. I then re-created the HTML of a single card inside of a `<template>` element just above the closing `</body>` tag.

```html
    <template id="card-template">
        <li class="photo-grid__item">
            <button class="button button_trash"></button>
            <img src="" alt="" class="photo-grid__image">
            <div class="photo-grid__content">
                <h3 class="photo-grid__title"></h3>
                <button class="button button_heart"></button>
            </div>
        </li>
    </template>
```

I won't fully go into the why's and how's of template tags here, but [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/template) is always a good place to start and then this series of articles on [CSS-TRICKS](https://css-tricks.com/an-introduction-to-web-components/) is an absolute gold-mine of information about Web Components. I've only just scratched the surface in terms of delving into these articles and will be referring back to them often as I try to gain a deeper understanding of Web Components and the Shadow DOM.

Suffice it to say that:

> A `<template>` **element** is a mechanism for holding HTML that is not to be rendered immediately when a page is loaded but may be instantiated subsequently during runtime using JavaScript. -- <cite>MDN</cite>

Instantiated subsequently during runtime using JavaScript you say? 😕

My understanding of this was that I'd need to use JavaScript to loop through the aforementioned array and then populate the source and alt attributes of the image element `<img src="" alt="" class="photo-grid__image">` within the template (and the text content of the header tag `<h3 class="photo-grid__title"></h3>` with the corresponding values from the array. Here's how that went down:

```javascript
// Add six initial cards on load
window.onload = (event) => {
    initialCards.forEach(function (item) {
        const cardTemplate = document.querySelector('#card-template').content;
        const cardElement = cardTemplate.cloneNode(true);
        const cardImage = cardElement.querySelector('.photo-grid__image');
        const cardTitle =  cardElement.querySelector('.photo-grid__title');
        cardImage.src = item.link;
        cardImage.alt = item.name;
        cardTitle.textContent = item.name;
        cardsContainer.append(cardElement);
    });
  };
```

So what did we do here? For each item within the array, we grabbed the HTML template and deeply cloned it (including everything within). We then grabbed the card image and title tags from within the template and linked the values from the array to the image and header tags. Bish, bash, bosh... I'll 🍻 to that!

## Add a form for adding a new card

Having just used a `<template>` element to achieve the previous outcome, I was now their biggest fanboy and immediately set about creating a template for the "New Place" form by copying and pasting the HTML for the existing "Edit Profile" form into a `<template>` element. 

> This is going to be a 🚶‍♂️ in the 🏞️  
>
> \-- <cite>Me</cite>

OM f@cking G when will I ever learn to stop getting carried away with myself 🤔?

Yes, it was easy to build the template and instantiate it via JavaScript as the button to instantiate the code is hard-onto the page. The problem arose when I tried to close the form. The close button would not work and I came to the conclusion that this was happening as the close button was part of the template and, therefore, not part of the page when it loads. 

I did the usual trawl through MDN, StackOverflow and Google and found a quasi-solution at [pawelgrzybek.com](https://pawelgrzybek.com/cloning-dom-nodes-and-handling-attached-events/) but it involved making use of inline events. It worked, but it just felt a bit "hacky" to me and I wasn't sure if it would be accepted by the code review team at Yandex. I started getting a bit p@ssed-off and decided it was time to 📱 a friend.

In times like these I always reach out to one of the experienced mentors - Alex. 

<iframe width="575" height="400" frameborder="0" allowtransparency="true" allowfullscreen="allowfullscreen" style="border: none;" src="https://share.getcloudapp.com/5zu1GQn1?embed=true"></iframe>

As you can see, Alex basically informed me that I was probably going the hard way about it and that I should probably just add the form HTML to the page directly and then toggle a visibility class via JavaScript attached to the click event on the "Add" and "Close" buttons. I went ahead and did this and  it worked but, again, it just felt  a little bit "hacky". I'm not saying that it is a hack because I really don't think it is. It just felt like it to me as I hadn't had the technical ability to pull the `<template>` element solution off and that didn't sit well with me.

I decided that, as the form would only ever need to be generated or removed dynamically, it should be done in JavaScript. Here's the code to create the form (including the modal/dialog):

```javascript
//Create add form
function addFormCreate () {
    const dialog = document.createElement("div");
    const closeButton = document.createElement("button");
    const header = document.createElement("h2");
    const form = document.createElement("form");
    const titleLabel = document.createElement("label");
    const titleInput = document.createElement("input");
    const urlLabel = document.createElement("label");
    const urlInput = document.createElement("input");
    const submitButton = document.createElement("button");
    dialog.classList.add('popup__dialog', 'popup__dialog_add')
    closeButton.classList.add('popup__close', 'popup__close_add')
    header.classList.add('content-title');
    header.textContent = "New Place";
    form.classList.add('form', 'form_add');
    titleLabel.classList.add('form__label');
    titleLabel.textContent = "Title";
    titleInput.classList.add('form__input', 'form__input_title');
    titleInput.type = "text";
    titleInput.name = "title";
    titleInput.placeholder = "Title";
    titleInput.required = true;
    urlLabel.classList.add('form__label');
    urlLabel.textContent = "Image URL";
    urlInput.classList.add('form__input', 'form__input_url');
    urlInput.type = "text";
    urlInput.name = "url";
    urlInput.placeholder = "Image URL";
    urlInput.required = true;
    submitButton.classList.add('button', 'button_submit');
    submitButton.type = "submit";
    submitButton.textContent = "Save";
    form.append(titleLabel, titleInput, urlLabel, urlInput, submitButton);
    dialog.append(closeButton, header, form);
    popup.append(dialog);
}
```

37 lines of code - and we're not stopping there! Here's the code for toggling the visibility of the form:

```javascript
//Toggle visibility of add form
function addFormVisibility () {
    const addFormDialog = popup.querySelector('.popup__dialog_add');
    addFormDialog.classList.toggle('popup__dialog_visible');
}
```

We also need to clear the form out once it's been submitted:

```javascript
// Clear form after submit
function addFormClear () {
    const titleInput = document.querySelector('.form__input_title');
    const urlInput = document.querySelector('.form__input_url');
    urlInput.value = "";
    titleInput.value = "";
}
```

And then add event listeners to the "Add New Place" button:

```javascript
document.addEventListener('click', function (evt) {
    if ( evt.target.classList.contains( 'button_add' ) ) {
        popupToggle();
        addFormCreate();
        addFormVisibility();
    }
}, false);
```

And the "Save" button:

```javascript
document.addEventListener('submit', popupToggle);
document.addEventListener('submit', addFormVisibility);
document.addEventListener('submit', addFormClear);
```

Phew! I learned an awful lot along the way here - including the fact that you can add multiple functions to event listener that listens for a `"click"`, but you can only add one for an listener that listens for a `"submit"` - hence the three separate listeners above. Did it work? Yes... up to a fashion! The form rendered as expected, but I had inadvertently run into the same problem that I'd previously encountered with the `<template>` element in that I couldn't access the `"Save"` and `"Close"` buttons via event listeners as they aren't present when the page is rendered. Fuuuuuuming 😤!

I got back onto Google and came across the concept of event delegation and this seemed to be the avenue that would lead to the eventual solution but none of the examples I came across really helped me link my situation to them in a way that helped me solve my problem. Then I struck gold with this article on: [Attaching event handlers to dynamically created elements](https://ultimatecourses.com/blog/attaching-event-handlers-to-dynamically-created-javascript-elements). It was miles simpler than I thought! All I needed to do was to include the event handler, and function we want to assign to it, inside the function that creates the element as follows:

```
 form.onsubmit = addFormSubmit; // Attach the event!
```

All we needed was one more line at the end of our 37 line function `addFormCreate` and we'd use this line to link the `onsubmit` event to the `addFormSubmit` function. Happy days! Of course, this now begs the question as to whether I should try to go back and solve the problem using a `<template>` element only this time armed with the right knowledge?  

## Develop a feature that will let users add custom cards

Actually, the code for this is tied together with the creation of the form, as detailed above, and I may need to separate these concerns as I move forward so for now I'll just show you that it works and we'll I'll try and address any potential improvements over the course of the next week:



<iframe width="575" height="400" frameborder="0" allowtransparency="true" allowfullscreen="allowfullscreen" style="border: none;" src="https://share.getcloudapp.com/z8uxZy5D?embed=true"></iframe>

## Conclusion

I learned so much this week and can honestly say that I haven't ever written as much JavaScript in the course of a week before in all my life. I feel like I've taken another massive step forwards and I can't wait to tackle the remaining items on the list over the course of the next week.