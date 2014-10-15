# Creating subtle UI details using Midnight.js, Wow.js and Animate.css

![Midnight.js](http://aerolab.github.io/subtle-animations/assets/midnight.jpg)

Creating animations in CSS or Javascript is often annoying and/or time-consuming, so most people tend to pay a lot of attention to the content that’s below “the fold" (“the fold" is quickly becoming an outdated concept, but you know what I mean).

I’ll be covering a few techniques to help add some nice touches to your landing pages that only take a few minutes to implement and require pretty much no development work at all.

To create a base for this project, I put together a bunch of photographs from https://unsplash.com/ with some text on top so we have something to work with. 

**Download the files from [http://aerolab.github.io/subtle-animations/assets/basics.zip](http://aerolab.github.io/subtle-animations/assets/basics.zip) and put them in a new folder.**

*You can also check out the final result at [http://aerolab.github.io/subtle-animations](http://aerolab.github.io/subtle-animations/)*.


## Dynamically change your fixed headers using Midnight.js

If you took a look at the demo site, you probably noticed that the minimalistic header we are using for “LoremIpsum" becomes illegible in very light backgrounds. When this happens in most sites, we typically end up putting a background on the header, which usually improves legibility at the cost of making the design worse.

**Midnight.js [http://aerolab.github.io/midnight.js/](http://aerolab.github.io/midnight.js/)** is a jQuery plugin that changes your headers as you scroll, so the header always has a design that matches the content below it. This is particularly useful for minimalistic websites, as they often use transparent headers. 

Implementation is quite simple, as the setup is pretty much automatic. Start by adding a fixed header into the site. The example has one ready to go:

```html
<nav class="fixed">
  <div class="container">
    <span class="logo">A How To Guide</span>
  </div>
</nav>
```

Most of the setup comes in specifying which header corresponds to which section. This is done by adding **data-midnight="your-class"** to any section or piece of content that requires a different design for the header.

For the first section, we’ll be using a white header, so we’ll add **data-midnight="white"** to this section *(it doesn’t have to be only a section, any large element works well)*.

```html
<section class="fjords" data-midnight="white">
  <article>
    <h1>Adding Subtle UI Details</h1>
    <p>Using Midnight.js, Wow.js and Animate.css</p>
  </article>
</section>
```

In the next section, which is a photo of ships in very thick white fog, we’ll be using a darker header to help improve contrast. Let’s use **data-midnight="gray"** for the second one, and **data-midgnight="pink"** for the last one, so it feels more in line with the content:

```html
<section class="ships" data-midnight="gray">
  <article>
    <h1>Be quiet</h1>
    <p>I'm hunting wabbits</p>
  </article>
</section>

<section class="puppy" data-midnight="pink">
  <article>
    <h1>OMG A PUPPY &lt;3</h1>
  </article>
</section>
```

Now we just need to add some css rules to change the look of the header in those cases. We’ll just be changing the color of the text for the moment, so open up **css/styles.css** and add the following rules:

```css
/* Styles for White, Gray and Pink headers */
.midnightHeader.white { color: #fff; }
.midnightHeader.gray { color: #999; }
.midnightHeader.pink { color: #ffc0cb; }
```

Last but not least, we need to include the necessary libraries. We’ll add two libraries right before the end of the body: **jQuery** and **Midnight.js** (they are included in the project files inside the js folder):

```html
<script src="js/jquery-1.11.1.min.js"></script>
<script src="js/midnight.jquery.min.js"></script>
```

And right after that we start Midnight.js on document.ready, using **$('nav.fixed').midnight()** (you can change the selector to whatever you are using on your site):

```html
<script>
$(document).ready(function(){
  $('nav.fixed').midnight();
});
</script>
```

If you check the site now, you’ll notice that the fixed header gracefully changes color when you start scrolling into the ships section. It’s a very subtle effect, but it helps keep your designs clean.

### Bonus Feature!

It’s possible to completely change the markup of your header just for a specific section. It’s mostly used to add some visual details that require extra markup, but it can be used to completely alter your headers as necessary. In this case, we’ll be changing the “logo" from “LoremIpsum" to “Shhhhhhhhh" on the ships section, and a bunch of hearts for the part of the puppy, for additional bad comedy.

To do this, we need to alter our fixed header a bit. **First we need to identify the “default" header** (all headers that don't have custom markup will be based on this one), and then add the markup for any custom headers, like the gray one. 

This is done by creating multiple copies of the header and wrapping them in **.midnightHeader.default**, **.midnightHeader.gray** and **.midnightHeader.pink** respectively:

```html
<nav class="fixed">
  <div class="midnightHeader default">
    <div class="container">
      <span class="logo">A How To Guide</span>
    </div>
  </div>
  <div class="midnightHeader gray">
    <div class="container">
      <span class="logo">Shhhhhhhhh</span>
    </div>
  </div>
  <div class="midnightHeader pink">
    <div class="container">
      <span class="logo">❤❤❤ OMG PUPPIES ❤❤❤</span>
    </div>
  </div>
</nav>
```

If you test the site now, you’ll notice that the header not just changes color, but it also changes the “name" of the site to match the section, which gives you more freedom in terms of navigation and design.


## Simple animations with Wow.js and Animate.css

**Wow.js [http://mynameismatthieu.com/WOW/](http://mynameismatthieu.com/WOW/)** looks more like a toy than a serious plugin, but it’s actually a very powerful library that’s extremely easy to implement.

Wow.js lets you animate things as they come into view. For instance, you can fade something in when you scroll to that section, letting users enjoy some extra UI candy. You can pick from a large set of animations from Animate.css [http://daneden.github.io/animate.css/](http://daneden.github.io/animate.css/) so you don’t even have to touch the CSS (but you can still do that if you want).

To get Wow.JS to work we have to include just two things:

**Animate.css**, which contains all the animations we need. Of course, you can create your own, or even tweak those to match your tastes. Just add a link to animate.css in the <head> of the document:
```html
<link rel="stylesheet" href="css/animate.css" />
```

And **Wow.JS**. This is simply just including the script and initializing it, which is done by adding the following just before the end of the document:
```html
<script src="js/wow.min.js"></script>
<script>new WOW().init()</script>
```

That’s it! To animate an element as soon as it gets into view, **you just need to add the .wow class to that element**, and then any animation from Animate.css (like .fadeInUp, .slideInLeft, or one of the many options available at [http://daneden.github.io/animate.css/](http://daneden.github.io/animate.css/)). 

For example, to make something fade in from the bottom of the screen, you just have to add wow fadeInUp. Let’s try this on the <h1> our first section:

```html
<section class="fjords" data-midnight="white">
  <article>
    <h1 class="wow fadeInUp">Adding Subtle UI Details</h1>
    <p>Using Midnight.js, Wow.js and Animate.css</p>
  </article>
</section>
```

If you feel like altering the animation slightly, you have quite a bit of control over how it behaves. For instance, let’s fade in the subtitle, but do it a bit later, so it follows a sequence. We can use **data-wow-delay="0.5s"** to make the subtitle wait for half a second before making its appearance:

```html
<section class="fjords" data-midnight="white">
  <article>
    <h1 class="wow fadeInUp">Adding Subtle UI Details</h1>
    <p class="wow fadeInUp" data-wow-delay="0.5s">Using Midnight.js, Wow.js and Animate.css</p>
  </article>
</section>
```

We can even tweak how long the animation takes by using **data-wow-duration="1.5s"**, so it lasts a second and a half. This is particularly useful in the second section, combined with another delay:

```html
<section class="ships" data-midnight="gray">
  <article>
    <h1 class="wow fadeIn" data-wow-duration="1.5s">Be quiet</h1>
    <p class="wow fadeIn" data-wow-delay="0.5s" data-wow-duration="1.5s">I'm hunting wabbits</p>
  </article>
</section>
```


We can even repeat an animation a few times. Let’s make the last title shake a few times as soon as it gets into view with **data-wow-iteration="5"**. We'll take this opportunity to use all the properties, like **data-wow-duration="0.5s"** to make each shake last half a second, and we'll also add a large delay for the last piece so it appears after the main animation has finished.

```html
<section class="puppy">
  <article>
    <h1 class="wow shake" data-wow-iteration="5" data-wow-duration="0.5s">OMG A PUPPY &lt;3</h1>
    <p class="wow fadeIn" data-wow-delay="2.5s">Ok, this one wasn't subtle at all</p>
  </article>
</section>
```


That’s pretty much all there is to know about using Midnight.js, Wow.js and Animate.css! All you need to do now is find a project and experiment a bit with different animations. It’s a great tool to add some last-minute eye candy and -as long as you don’t overdo it- looks fantastic in most sites. I hope you enjoyed the article!
