---
title: A Week of Firsts
date: 2020-04-20T06:40:33.500Z
tags:
  - blog
  - learning
---
I've been taking part in beta-testing the the Web Developer track of the Practicum by Yandex educational platform since 3rd February 2020 and I consider myself exceptionally fortunate to be a part of it. I'm part of the Lime group and, so far, we've completed 5 amazing projects for our portfolios. 

For our latest project we were split into pairs and asked to code the front-end of a simple 2-3 page app using HTML, CSS and JS. There was a choice of four different projects:

* 🚗 Car eCommerce app
* 🍔 Food eCommerce app
* 🎥 Movie reviews app
* 🎵 Music streaming app

I wanted to build the music streaming app and I managed to get myself assigned to Beethoven team along with the super-talented Jayme Waye 🎉. Here's the link to the Figma design file that we were tasked with turning into a prototype:

[Music Streaming App Design File](https://www.figma.com/file/rRE5kHZSGzj2XSd0gZQgrl/Music-Player-Box-Template-Copy?node-id=0%3A1)

Every day is a school day 🎓 and this is what helps me get out of bed in the morning. I ❤️ learning and the feeling of being pushed outside of your comfort zone and this week I learned some things that I feel it's worth making a record of:

1. How to style a HTML progress bar
2. How to loop through an array in JavaScript and selectively apply CSS classes
3. How to collaborate on code in GitHub, set up a pull request and review somebody else's code

## How to style a HTML progress bar

If you check out the design file linked above, you'll see that the first or home screen of the app looks quite a bit more complicated to design/code that the second or player screen. I gave Jayme the chance to specify which screen she'd like to code and she said she didn't have a preference so I instantly reverted to type and chose what I felt would be the easier option - the player screen 👇 (sorry Jayme 🤭).

![A music streaming app design in Figma](/images/music-app-figma.png "The design file for our app")

The progress bar was the only unknown entity to me on this screen and I imagined it had been included as part of the design as the mentors knew it would be a bit of a pain in the ass to style.

As with most things in life, particularly web/software dev, it's always easier to stand on the shoulders of giants and so I turned to the #1 skill of the modern developer - I Googled it 😂. I came across this super-comprehensive article by Pankaj Parasar on CSS-TRICKS:

[The HTML5 Progress Element](https://css-tricks.com/author/pankajparashar/)

Pankaj had also created a Pen on CodePen:

[Skillset using HTML5 progress bars with CSS3 animations](https://codepen.io/team/css-tricks/pen/PNNQxm "Skillset using HTML5 progress bars with CSS3 animations")

Let me be clear here though, this wasn't just a straight-forward copy and paste job! Whilst Pankaj had been extremely thorough, making sure the markup and styling were as cross-browser compatible as possible whilst also being backwards compatible, he'd also added lots of styling that I'd need to remove or change in order to stay on-brief.

In terms of the HTML, I chose to use the method that would designed to provide a fallback for browsers that don't support the progress element as I felt that this was the most inclusive pattern. The only difference between Pankaj's code and mine here was the addition of BEM-style CSS classes that I would use to help style and structure my CSS:

```html
<progress max="100" value="68" class="track__progress">
  <div class="track__span-box">
    <span class="track__span">Progress: 68%</span>
  </div>
</progress>
```

The CSS was where I had to make the most changes. On top of the visual styling changes that I've previously mentioned, Pankaj hadn't used BEM naming structure or file-nesting architecture and both of these were prerequisites of my project. Here's the CSS I eventually settled on for the progress element itself:

```css
  
.track__progress[value] {
  /* Reset the default appearance */
  
    -webkit-appearance: none;
       -moz-appearance: none;
            appearance: none;
  
  /* Get rid of default border in Firefox. */
    border: none;
  
    width: 12.6875rem;
    height: .25rem;
    background-color: var(--color-grey);
    color: var(--color-primary);
    position: relative;
}

.track__progress[value]::-webkit-progress-bar {
  /*style the progress element container. */
    background-color: var(--color-grey);
    border-radius: 3px;
}

.track__progress::-webkit-progress-value {
  /*style the value inside the progress element container. */
    background-image:none;
    background-color:var(--color-primary);
}

.track__progress::-moz-progress-bar {
  /*style the progress bar value in Firefox (container can't be styled (yet)) */
    background-color: var(--color-primary);
  }
```

I also had to add styling for the span container:

```css
.track__span-box {
    background-color: var(--color-grey);
    width: 203px;
    height: .25rem;
  }
```

And the span element:

```css
.track__span {
    background-color: var(--color-primary);
    display: block;
    text-indent: -9999px;
  }
```

These elements were then pulled together within the parent block:

```css
@import url('./__progress/track__progress.css');
@import url('./__span-box/track__span-box.css');
@import url('./__span/track__span.css');

.track {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 2rem;
}
```

And that was that! The app can be found on GitHub Pages if you'd like to take a look:

[Music Streaming App](https://jimiryquai.github.io/music_player_app/player.html)

## How to loop through an array in JavaScript and selectively apply CSS classes

Once I'd got my work to the work to the point where I felt it satisfied the brief, I started to wonder how I could stretch myself further. I considered adding audio files that would play/pause when the Play button was pressed and felt like I could actually get this done but I wouldn't have been happy without also being able to get the Rewind/Fast Forward buttons working and I wasn't so confident about that. In the end, I took what I thought would be an easier options and decided to try and implement