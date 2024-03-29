# HTML
## Contributors
Point of contact for discussions and evolutions of the HTML-consensus: Mathieu Spillebeen

Supported by:
 - Frederick Roegiers 
 - Tim De Geeter
 - Wachem Huyge
 - Miguel De Pelsmaeker
 - Tim De Paepe
 - No-one else yet :) Be the next! ;)

## Principles
 - The lean-principle: `www` doesn't stand for the Wealthy White West, keeping the loadtimes and weight of ouw interfaces low means that we keep it as accessible towards a world wide audience, and we keep our carbon footprint to a minimum.
 - The robust-principle: An interface should have the least amount of reliabilities that could end up breaking the interface or making your content not accessible to your audience.

## Don't start paths with / if the work won't be hosted on a server
One of the first hurdles, students experience when starting to write HTML is when writing relative paths. So we should unify how we teach them. 

Starting a relative path with `/` will only work when the files are viewed from a server(-emulated) environment. Evaluating the result of their code as teachers is very tedious, if we can't just double click the `index.html` but instead need to set their project up in a way that we have our local server setup from the same folder as each student individually.

Once the student is delivering their project or test through a server, it's ok to use "/" in the beginning of url's

<!-- panels:start -->
<!-- div:panel--left panel--dont -->
```html
<!-- HTML-file in a zipped project -->
<img src="/folder-in-root/image.png" alt="an example">
```
Don't start with a "/" if your work won't be on a server.

<!-- div:panel--left panel--do -->
```html
<!-- HTML-code in a zipped project -->
<img src="folder-in-root/image.png" alt="an example">
<img src="../folder-in-root/image.png" alt="an example">
<img src="../../folder-in-root/image.png" alt="an example">

<!-- HTML-code in a hosted project on a server -->
<img src="/image.png" alt="an example">
```
Only start with "/" on server-hosted pages.

<!-- div:panel--left panel--do -->
```html
	
<head>
  <!-- This will prefix all the relative url's with "../" -->
  <base href="../">
</head>
 
<body>
  <ul>
    <li><a href="index.html">Home</a></li>
    <li><a href="pages/about.html">About</a></li>
    <li><a href="pages/contact.html">Contact</a></li>
  </ul>  
</body>
```
Use the base-tag for nesting HTML-files.
<!-- panels:end -->

## Class-naming conventions
HTML is an international language that has adopted the English language in it's core. When naming elements, we should always keep to the English language.
Naming things is hard, very hard. The logic here should be to make pragmatic use of BEM and utility classes, or in other words: KISS (Keep It Simple Stupid) and use [BEM-methodology](https://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/) in the use-cases where it is actually helpfull.
<!-- panels:start -->
<!-- div:panel--left panel--dont -->
```html
<!-- Don't capitalise classnames -->
<div class="MyBlock"></div>

<!-- Don't write in Dutch -->
<div class="blokje"></div>

<div class="cards">
  <div class="cards__card">...</div>
  
  <div class="cards__card cards__card--blue"></div>
 
  <div class="cards__card cards__card--text-centered"></div>
</div>
```
Don't overuse BEM.

<!-- div:panel--right panel--do -->
```html
<div class="cards">
  <div class="card">...</div>
  
  <div class="card card--blue"></div>
 
  <div class="card text-centered"></div>
</div>
```
Keep it as simple as possible.
<!-- panels:end -->

## Icon fonts
Icon fonts such as the wildly popular Font Awesome are amazing in terms of iconograpgy. However, implementing them as an icon font, means that they are [notoriously bad for accessibility](https://www.irigoyen.dev/blog/2021/02/17/stop-using-icon-fonts/) and can lead to some frustrating experiences for those who rely on assistive technologies.

They also break the lean-principle, as they aren't cheap to download.

When you want to use an icon-font, download the icons seperately, and use them as SVG's.


## Libraries
Using libraries is fine, but keep it as lean as possible. And only if the alternative is much worse. 

For example: 
 - If you only are using Bootstrap's grid system. Don't include everything of Bootstrap, but only include the code that supplies the grid. 
 - If you want to show Tailwind, keep it lean and don't use it to an extend that students no longer know what it is replacing. The standards of the web will stay, but Tailwind might be gone by the time they finish their learning curve with us.

## Cross-domain dependencies
Limit the dependencies from other domains, where possible. trusting on other domains of people or organisations you don't know, means that you are on a thin line of trust-based development. [CDN's have been debunked for being faster for a long time now](https://csswizardry.com/2019/05/self-host-your-static-assets/), host your assets locally!


## Tabs vs Spaces
Tabs are more accessible than spaces, so please use tabs in your code examples.

## Formatting
If you want your editor to wrap the text for easier editor, you can toggle the setting **View: Toggle word wrap**.

<!-- panels:start -->
<!-- div:panel--left panel--dont -->
```html
<p>
  This is some very long text, but if beatify isn't 
  correctly configured, it will create multiple lines for 
  this paragraph.
</p>
```
Don't use multiple lines for running text.

<!-- div:panel--left panel--do -->
```html
<p>
  This is some very long text, but if beatify isn't correctly configured, it will create multiple lines for this paragraph.
</p>
```
Only use 1 line for running text
<!-- panels:end -->

