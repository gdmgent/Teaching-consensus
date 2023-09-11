# CSS
## Contributors
Point of contact for discussions and evolutions of the CSS-consensus: Mathieu Spillebeen

Supported by:
 - Frederick Roegiers 
 - Tim De Geeter
 - Wachem Huyge
 - Miguel De Pelsmaeker
 - Dieter De Weirdt
 - No-one else yet :) Be the next! ;)

## Principles
When teaching CSS, we should follow a few key principles.
 - Accessibility is the norm, not an afterthought
 - Responsiveness is not an option, it is the foundation of CSS.
 - Readability and maintainability are more important then keeping your code DRY.
 - New specifications of CSS should only be taught when it is **certain** that the spec will be widely used by the time the student finishes their education with us.

## Terminology
### Font-scaling
<!-- panels:start -->
<!-- div:panel--left -->
<video controls>
  <source src="assets/media/chrome-font-scaling.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

<!-- div:panel--right -->
The most preferred way of providing a readable website. We can increase the default font size in our browser settings. Essentially, you can think of font scaling as changing the definition of 1 rem. In an ideal world, a user needs to set this in their browser once, and all fonts of all the websites will be readable for that user.
<!-- panels:end -->

### Zooming
<!-- panels:start -->
<!-- div:panel--left -->
<video controls>
  <source src="assets/media/chrome-zoom.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

<!-- div:panel--right -->
When font-scaling was't enough to make the font readable enough, a user can use zoom in or out by pressing `⌘` + `+` on MacOS, or `ctrl` + `+` on Windows/Linux. This way it's possible to view the mobile version on a desktop as all the units scale up. This is still a very good option for users, as all the content will stay accessible.
<!-- panels:end -->

### Browser-zooming
<!-- panels:start -->
<!-- div:panel--left -->
<video controls>
  <source src="assets/media/browser-zooming.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

<!-- div:panel--right -->
We can also zoom within a browser, when the previous 2 zooming mechanisms weren't sufficient. This type of zooming can be done as a last resort by pinch and zoom. It will essentially apply a multiple to every unit, including pixels. It affects everything except viewport units (like vw and vh). This has the nasty side-effect that the user will have both horizontal and vertical sidebars and will only view a fraction of the website. 
<!-- panels:end -->


## CSS Units 
There are a lot of different units available in CSS, all these units come with there own set of possiblities and problems. In order to make the learning curve for students as flat as possible, aggreeing on which units are to be used when, would help avoid a lot of confusions.

### An overview
#### Pixel
So, the `px` unit is a bit of a lie. It doesn't actually map neatly onto hardware pixels.

If you look at a modern display under a microscope, you'll realize that they aren't made up of crisp little R/G/B rectangles anymore. There has always been a distinction between the physical pixels in a screen and the software pixels we write in CSS. Every time a user changes their screen's resolution or zooms in, they're changing how software pixels map onto hardware pixels.

This doesn't mean that we shouldn't use pixels, but it also doesn't mean we should use it for everything.

#### Em's
The em unit is an interesting fellow. It's a relative unit, based on the element's calculated font size.
<iframe height="300" style="width: 100%;" scrolling="no" title="Untitled" src="https://codepen.io/mathieuspil/embed/xxWOywJ?default-tab=&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/mathieuspil/pen/xxWOywJ">
  Untitled</a> by Mathieuspil (<a href="https://codepen.io/mathieuspil">@mathieuspil</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

Note: To make it easier to understand how the `em` unit works, we're using pixel-based font sizes here. As we'll learn shortly, however, this is a bad idea. Please don't do this in real applications!

#### Rem's
Rem's were introduced because there was a common frustrating issue with the em unit: it compounds...
For example, consider the following snippet:

```html
<style>
  main {
    font-size: 1.125em;
  }
  article {
    font-size: 0.9em;
  }
  p {
    font-size: 1.25em;
  }
</style>

<main>
  <article>
    <p class="intro">What size am I?</p>
  </article>
</main>
```

How large, in pixels, is that .intro paragraph font?

To figure it out, we have to multiply each ratio. The root font size is 16px by default, and so the equation is `16px × 1.125 × 0.9 × 1.25`. The answer is 20.25 pixels. Essentially, we need to multiply every `em` value in the tree until we either hit a "fixed" value (using pixels), or we make it all the way to the top of the tree. Which is incredibly weird to calculate or to predict by looking at the CSS as a developer.

The `rem` unit is like the `em` unit, except it's always a multiple of the font size on the root node, the `<html>` element. It ignores any inherited font sizes, and always calculates based on the top-level node.

Documents have a default font size of 16px, which means that 1rem has a “native” value of 16px. This value however is user-configurable, by font-scaling!

### Typography
#### Font-size 
`rem` respects both font scaling and zooming, and is therefor the preffered way of how we should be defining font-sizes.

<!-- panels:start -->
<!-- div:panel--left panel--dont -->
```css
.selector {
  font-size: 32px; /* Doesn't respect browser accessibility settings */
  font-size: 2em; /* Hard to know on first glance what this value this will be once rendered */
}
```
In general Don't use pixels or em's.

<!-- div:panel--right panel--do -->
```css
.selector {
  font-size: 2rem;
}
```
Use rems for font-size.

<!-- div:panel--dont -->
```css
html {
  font-size: 20px; 
  /* or */
  font-size: 2rem; 
}
```
Don't overwrite the font-size on the root-element
<!-- panels:end -->

**Exception use-case**
There are use-cases for within components where you will want to use ems if you want values to intentionally compound relative to font-sizes of itself or of it's nearest parent. Make use of this compounding effect sparingly, as it can add quite a bit of complexity to the learning curve of students. 
<!-- panels:start -->
<!-- div:panel--do -->
```css
.selector {
  /* Still use rem's to base em's upon! */
  font-size: 2rem;
}

.selector__child {
  font-size: 1.2em;  /* results in 2rem * 1,2 */
  padding: 2em;      /* results in 2rem * 1,2 * 2 */
}

.selector__child__grandchild {
  font-size: 0.5em;  /* results in 2rem * 1,2 * 0,5 */
  padding: 2em;      /* results in 2rem * 1,2 * 0,5 * 2 */
}
```
Use the em-unit only where it has a clear advantage
<!-- panels:end -->

#### Line-height
Line-height are always relative to the font-size of the text itself. We should therefor always use a relative unit. If we use percentages, line-height will behave as it was intended: relatively to the font size.

<!-- panels:start -->
<!-- div:panel--left panel--dont -->
```css
.selector {
  font-size: 1rem;
  
  line-height: 20px;
  /* or */
  line-height: 1.4rem;
}
```
Don't use a unit that don't keep the link to it's own font-size.

<!-- div:panel--right panel--do -->
```css
.selector {
  font-size: 1rem;
  line-height: 140%;
}
```
Percentage-based line-height won't give you trouble if you change the font-size.
<!-- panels:end -->

#### Letter-spacing
Letter-spacing (or word-spacing) should always use the same unit as font-size. And because we have concluded font-size to be defined in `rem`, so should the letter-spacing.
<!-- panels:start -->
<!-- div:panel--left panel--dont -->
```css
.selector {
  font-size: 1rem;
  letter-spacing: 0.2px;
}
```
Don't use (px) for letter spacing.

<!-- div:panel--right panel--do -->
```css
.selector {
  font-size: 1rem;
  letter-spacing: 0.0125rem;
}
```
Use rem for letter-spacing.
<!-- panels:end -->

### Layout
#### Padding for textual elements
People that crank up the font-scaling, still want an excellent looking design. When designing a button for example, the whitespace within the button should be relative to the font-size of that button.
<!-- panels:start -->
<!-- div:panel--left panel--dont -->
```css
button {
  font-size: 2rem;
  padding: 8px 16px;
}
```
Don't use (px) for padding on buttons.

<!-- div:panel--right panel--do -->
```css
button {
  font-size: 2rem;
  padding: 0.5rem 1rem;
}
```
Use rem for padding on buttons.
<!-- panels:end -->

<iframe height="300" style="width: 100%;" scrolling="no" title="Padding on textual elements" src="https://codepen.io/mathieuspil/embed/jOzMEoq?default-tab=result&theme-id=dark" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href="https://codepen.io/mathieuspil/pen/jOzMEoq">
  Padding on textual elements</a> by Mathieuspil (<a href="https://codepen.io/mathieuspil">@mathieuspil</a>)
  on <a href="https://codepen.io">CodePen</a>.
</iframe>

#### Width for textual elements
When defining `width` and `max-width` on elements that impact line-length, it's important for readability, that a single line shouldn't exceed 75 characters. Defining widths in regular-old pixels would break the readability for people that have tweaked their font-scaling.
<!-- panels:start -->
<!-- div:panel--left panel--dont -->
```css
p {
  width: 100%;
  max-width: 640px;
}
```
Don't use (px) for width.

<!-- div:panel--right panel--do -->
```css
p {
  width: 100%;
  max-width: 40rem;
}
```
Use rem for max-width.
<!-- panels:end -->


#### Media queries
We're used to thinking of `media queries` in terms of mobile/tablet/desktop, however in the ever evolving landscape of possible harware devices, we should be thinking more in terms of **available space**.
In the context of breakpoints for elements that contain text, the available space will be relative to the font-scaling of the user. 

A design for mobile is usually a design where text gets almost all the horizontal space of the screen, if a user cranks up their default font-size, the mobile design shouldn't only be shown up until `800px`, but up until the 800px-equivalent for font-scaling users: `50rem`.
<!-- panels:start -->
<!-- div:panel--left panel--dont -->
```css
@media (min-width: 800px) {
  ...
}
```
Don't use (px) for media queries.

<!-- div:panel--right panel--do -->
```css
@media (min-width: 50rem) {
  ...
}
```
Use rem for media queries.

<!-- panels:end -->

#### Mobile-first or Desktop-first?
Use whichever makes most sense to the context of the project, but don't mix them within a project, as that makes the predictability of the outcome of the CSS unnecessarily complicated.

### White space
The question we should ask ourselves here is: should the value grow, when the user makes the default font-size bigger?
If yes then we should use `rem`, if not we should use `px`.
#### Horizontal padding between edge of the screen and content
If the user makes the default font-size bigger, then chances are that less words will fit on their mobile screen. Therefor, we shouldn't make the problem worse by adding more horizontal spacing between the edge of the screen en the content.
<!-- panels:start -->
<!-- div:panel--left panel--dont -->
```css
.layout-container {
  padding: 0 1rem; /* Doesn't need to grow along with the font-size */
}
```
Don't use rems.

<!-- div:panel--right panel--do -->
```css
.layout-container {
  padding: 0 16px; /* Doesn't need to grow along with the font-size */
}
```
Do use pixels
<!-- panels:end -->


## CSS architecture
### Multiple files
Using multiple files to structure your CSS is the preferred way in an HTTP2 world. Please only abstract to multiple files when it has a clear advantage. 

### Class-based theming
Theming using id's is not scalable, and we should avoid them as much as possible. 

### Media queries
Building on top of the principle of class-based theming en possible multiple files, we should group our media-queries right below the class that they will be overwriting. For the sake of simplicity, readability and maintainability.

An added advantage of not grouping media queries is also that not every component should *break* on the exact same breakpoint as another component.
<!-- panels:start -->
<!-- div:panel--left panel--dont -->
```css
.component-a {
  ...
}

.component-b {
  ...
}

.component-c {
  ...
}

@media (min-width: 50rem) {
  .component-a {
    ...
  }

  .component-c {
    ...
  }
}
```
Don't group media queries.

<!-- div:panel--right panel--do -->
```css
.component-a {
  ...
}
@media (min-width: 48rem) {
  .component-a {
    ...
  }
}

.component-b {
  ...
}

.component-c {
  ...
}
@media (min-width: 52rem) {
  .component-c {
    ...
  }
}
```
Repeat the media query whenever necessary.
<!-- panels:end -->

## Color
When designing interfaces, we currently use the basis of Refactoring UI. Colors that belong to the same hue are easier to identify if we write them out in the `hsl()` or `hsla()`-notation. While our choice of preference is to use `hsl()` or `hsla()`-notation, we shouldn't punish students that use different notations.
<!-- panels:start -->
<!-- div:panel--left panel--dont -->
```css
.selector {
  color: #127634;
  color: blue;
}
```
But it's not wrong to use other notations.

<!-- div:panel--right panel--do -->
```css
.selector {
  color: hsl(12, 50%, 30.1%);
  background: hsla(12, 50%, 30.6%, 0.4);
}
```
Preferably use hsl or hsla for colors as the default as much as possible.
<!-- panels:end -->

## Our custom CSS Reset
There are loads of CSS Reset's out there, but in order to smooth out the learning curve for our students we should use the same starting point. This has the advantage of no longer having to talk around loads of quircks of browsers, and getting straight to the fun bits.
Loads copied from [Josh Comeau's custom CSS reset](https://www.joshwcomeau.com/css/custom-css-reset/)

The latest version of Artevelde's reset.css can be downloaded from [gdm.gent/css](https://www.gdm.gent/css/) by students and teachers alike and is maintained on a [different Github repo](https://github.com/gdmgent/css/blob/main/docs/reset.css): 

## References
Loads copied from [a blogpost from Josh Comeau](https://www.joshwcomeau.com/css/surprising-truth-about-pixels-and-accessibility/ ). 
