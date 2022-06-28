# CSS Units
There are a lot of different units available in CSS, all these units come with there own set of possiblities and problems. In order to make the learning curve for students as flat as possible, aggreeing on which units are to be used when, would help avoid a lot of confusions.

## Typography
### Typography: Font-size 
We should give the user as much control as possible from an accessibility point of view. `rem` allows users to choose how big they want the default font-size to be on every browser without having to manually zoom in on every browser. 
[:speech_balloon: discussion](https://github.com/gdmgent/Teaching-consensus/issues/1)

:red_circle: Don't use pixels
```css
.selector {
  font-size: 32px; // Doesn't respect browser accessibility settings
  font-size: 2em; // Not maintainable on larger sizes.
}
```

:green_heart: Do use rem
```css
.selector {
  font-size: 2rem;
}
```

## White space
The question we should ask ourselves here is: should the value grow, when the user makes the default font-size bigger?
If yes then we should use `rem`, if not we should use `px`.
### White space: horizontal padding between edge of the screen and content
If the user makes the default font-size bigger, then chances are that less words will fit on their mobile screen. Therefor, we shouldn't make the problem worse by adding more horizontal spacing between the edge of the screen en the content.

:red_circle: Don't use rems
```css
.layout-container {
  padding: 0 1rem; // Doesn't need to grow along with the font-size
}
```

:green_heart: Do use pixels
```css
.layout-container {
  padding: 0 16px; // Doesn't need to grow along with the font-size
}
```
