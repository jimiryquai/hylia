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

As with most things in life, particularly web/software dev, it's always easier to stand on the shoulders of giants and so I turned to the #1 skill of the modern developer - I Googled it 😂. I came across this super-comprehensive article by Pankaj Parasar on CSS-TRICKS: [The HTML5 Progress Element](https://css-tricks.com/author/pankajparashar/). Pankaj had also created a Pen on CodePen: [Skillset using HTML5 progress bars with CSS3 animations](https://codepen.io/team/css-tricks/pen/PNNQxm "Skillset using HTML5 progress bars with CSS3 animations").

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

And that was that! The app can be found on GitHub Pages if you'd like to take a look: [Music Streaming App](https://jimiryquai.github.io/music_player_app/player.html).

## How to loop through an array in JavaScript and selectively apply CSS classes

Once I'd got my work to the point where I felt it satisfied the brief, I started to wonder how I could stretch myself further 🤔. I considered adding audio files that would play/pause when the Play button was pressed and felt like I could actually get this done but I wouldn't have been happy without also being able to get the Rewind/Fast Forward buttons working and I wasn't as confident about that. In the end, I took what I thought would be the easier option (surprise, surprise) and decided to try and implement a dark theme.

Why was I more confident about being able to implement this feature? I'll tell you why... because I follow the ridiculously-good [@hankchizljaw](https://twitter.com/hankchizljaw?lang=en) and he has a superb tutorial on his website [Piccalil.li](https://piccalil.li/tutorial/solution-002-toggle-switch/). Give him a follow on Twitter - heck, join his [Community](https://community.piccalil.li/) - it's gold believe me!

So I followed along with Andy's tutorial and also took a look at the website of another member of his community, Daniel Post. On his site [Daniel](https://danielpost.com/) has taken a slightly different approach to Andy in that he's created his toggle as a button rather a checkbox and he's also placed it inside of a modal popup. I decided to take a hybrid approach - use the code from Andy's tutorial and place the toggle inside a popup modal à la Daniel.

![A screenshot of Daniel Post's website showing his popup implementation](/images/daniel-pop-up.png "The amazing site of Daniel Post")

After a little bit of tinkering around I had a (semi) working implementation of the dark mode theme on my page:

![A screenshot of the music player with dark mode applied](/images/darkmode.png "Who turned the lights out?")

Can you spot the obvious mistake or omission here? Yep, that's right - my buttons and text are no longer visible. The polar opposite of accessibility and not what we want at all! I'm a beginner/upper beginner with JavaScript but I knew that I'd need to extend Andy's code and apply a `dark` class to every button on the page. The first thing I did was declare a variable that would store all the buttons as a list:

```javascript
const buttons = document.querySelectorAll('button');
```

I then further extended Andy's code by adding a `for` loop to apply the dark class to each item in this list:

```javascript
toggle.querySelector('input').addEventListener('change', evt => {
  if (evt.target.checked) {
    main.classList.add('main-content_dark');
    for (let i = 0; i < buttons.length; i++) {
        buttons[i].classList.add('button_dark');
    }
    return;
  }

  main.classList.remove('main-content_dark');
      for (let i = 0; i < buttons.length; i++) {
        buttons[i].classList.remove('button_dark');
    }
});
```

This did the trick in terms of making my buttons visible but it was also incomplete as a solution and had some unintended side-effects:

![An animated image showing dark mode being toggled on and off](/images/dark-toggle.gif "Houston... we have problems")

So there were three things going on:

1. The pause button was basically disappearing due to the dark class being applied.
2. The close button at the top of the popup (which is invisible and needs fixing) is flashing when the dark class is applied.
3. The text is still disappearing.

At this point I was a little bit stuck and turned to Google where I searched for "query selector all but one" (it should've actually been two but... 🤷‍♂️) and the first entry in the results was from the other search engine that every developer relies upon: [Stack Overflow](https://stackoverflow.com/questions/25605367/how-to-exclude-specific-class-names-in-queryselectorall): I had come across the `:(not)` selector before in CSS but didn't know that you could use it in JavaScript too. I amended my variable by chaining two `:not()` selectors to the button class and passed the classes of the buttons that I wanted to exclude in as parameters:

```javascript
const buttons = document.querySelectorAll('button:not(.button_play):not(.popup__close)');
```

I terms of the text, I took the really easy option of removing the colours that I had applied to them and allowing the global `color: inherit;` to do it's work. As you can see... it worked! 

![](/images/dark-mode-working.gif)

Technically this is a bit of a hack and in real terms it would have contradicted the brief in terms of text colours but I had other issues that needed resolving so I left this work on the feature/dark-mode branch and didn't merge with the develop branch within the GitHub repo. This feature will be revisited in the near future.

## How to collaborate on code in GitHub, set up a pull request and review somebody else's code

Up until this project I'd been the sole contributor on all of the projects I'd worked on. After setting up the repo on GitHub I invited to contribute and then created a develop branch:

```gitconfig
git checkout -b develop
```

This is where I set up the file structure and created my HTML framework. Once this was completed., I would then create a feature branch for each section of the layout and work on the CSS and JavaScript for each feature separately before merging back into develop.

Creating separate branches for features and making small, regular commits in this way was very helpful in terms of staying organised. One thing I became acutely aware of was the need to make sure to pull the latest code down from GitHub every morning or every time I'd stepped away from my computer for a while. This wasn't an established habit and I almost got caught out a couple of times only to see that Jayme had made changes to the code base in the meantime.

Once Jayme and I were relatively happy with our work it was time to set up a pull request and then invite two fellow students to review our work. The only issue was that I didn't have a clue how to do this. After much searching I came across this lifesaver of an article