# Responsive Web Design

Websites are viewed on all different sizes of screens from phones to laptops to large displays. When making a web page we do our best to make the page look great on any size display.
With print design, the task is easier, we know the final size when designing a poster or layout. With web design, we must design the page to respond to size of the screen. 
This is known as "Responsive Web Design" 
We can achieve this using only CSS. The html structure and content of the page doesn't change.
 
There are three major CSS patterns that can use to achieve this.  
- Media Queries
- Responsive Units
- Flexible Sizing

## Media Queries
Try this experiment: 
- Choose any webpage you frequent.
- Open up the dev tools
- Change the width of your view
- Observe what happens, note the pixel value of the width. Are there some pixel values where major "breaks" in the design happen?

To make this happen, we use a special type of CSS rule called a Media Query. Here is an example...

```css
@media only screen and (min-width: 768px) {
  /* css overrides to inside these {} */
  body {
    background-color: #f0c808;
  }
}
```
The background color of the body will be updated once the browser's width is 768px or larger. The rule will stay in place unless it is overridden about another later rule.

[Here](./tutorials/responsive-web/examples/queries/) is an interactive demo. [Here](/tutorials/responsive-web/examples/queries/style.css) is the code that makes that happen.

### Common Breakpoints
Here are common ranges used for breakpoints

| Device Type  | Breakpoint Range | Examples | 
| ------------- | ------------- |
| Mobile | 320px - 480px | Smartphones (portrait) |
| Tablet  | 481px - 768px |	Tablets (portrait), small laptops |
| Small Desktop | 769px - 1024px | Tablets (landscape), smaller laptops |
| Large Desktop | 1025px and up | Desktop monitors, larger laptops |

[source](https://dev.to/gerryleonugroho/responsive-design-breakpoints-2025-playbook-53ih)

## Responsive Units
When first learning CSS you might use a pixels (px) as a common unit for fonts, margins, and sizing elements. But pixels are static and therefore not responsive to what is happening on the page.

It is better to use *responsive units* that change based on what is happening on the page.

### Relative Units for Type
- `em`, Relative to the font-size of the element
  - `font-size: 2em;` means 2 times the size of the current parents font
- `rem`, Relative to font-size of the root element
  - `font-size: 2rem;` size will be 32px if html font-size is 16px
- `%`, defines the size as a percent of the parent
  - `font-size: 50%;` size will be 8px, 16 * 50% = 8

[Try it out](https://codepen.io/awdriggs/pen/myeYRLK?editors=1100)

For your page, choose your font sizes based on a proportional hierarchy.

Don't define a base font size in pixels like this:
```css
html {
  font-size: 10px;
}
```
Some people change set their browsers default size on purpose because of visual preferences. Setting a pixel size ignores their preference and makes your site less accessible.

Since more browsers have a default font size of 16px, so 1rem equals 16px, 2rem equals 32px and so on.

If you want your rem values to convert to easy pixel values, set the base font-size as a percent of the default.
```css
html {
  font-size: 62.5%; /* 62.5% of 16 is 10px */
}

h1 {
  font-size: 2.5rem; /* 2.5 * 10 is 25px */
}
```

If you want to change all the text sizes proportionally you can increase the base size font with a media query.
```css
@media only screen and (min-width: 768px) {
  /* css overrides to inside these {} */
  body {
    font-size: 100%; /* back to default, everything in rems will change in proportion. */
  }
}
```

### Relative Units for Sizing
Again, don't size elements as pixel values. This is too static. Instead we should use responsive units:
- %, defines the size as a percent of the parent.
  - `width: 50%;` the elements width will be 50% of the parents width.
- vw/vh, view width and view height come from the viewport size.
  - `width: 50vw;` the elements width will be 50% of the viewport.

Even use rems!
- `rem`, Relative to font-size of the root element
  - `margin: 2rem;` margin will be 32px if html font-size is 16px

[Try it out](https://codepen.io/awdriggs/pen/EaVzWbE)

### Dynamic View Height
On mobile `vh` often ignores the browser bars, so its not accurate and could leave gaps. New mobile-friendly `vh` units solve this.
- `svh` small viewport height, the minimum height (with bars visible).
- `lvh` large viewport height, the maximum height (bars collapsed).
- `dvh` dynamic viewport height, the current height (updates as bars show/hide).

So if you want an element to be the full height of the screen, you could this.
```css
.full-height {
  height: 100vh; /* fallback for older browsers */
  height: 100dvh; /* use dynamic size if supported */
}
```

## Flexible Sizing
Now that we know about all the responsive units, we can use those to dynamically control the size. 

### Minimum and Maximum Sizes
It is nice to control the minimum and maximum size so % base sizing doesn't get out of hand!
- `max-width` sets the maximum size that an element can be.
  - `max-width: 500px`, element never gets bigger than 500px.
- `min-width` sets the minimum size that an element can be.
  - `min-width: 500px`, element never gets smaller than 500px.

[Try it out!](https://codepen.io/awdriggs/pen/LEpoWoa?editors=1100)

### Clamp
Clamp is a newish CSS function, it picks a value that’s never smaller than min, never larger than max, and otherwise uses your preferred value.

`property: clamp(min, preferred, max);`

One line for fluid values with hard stops (no media queries) and you can mix units (px, rem, vw, etc.).

```css
.card {
  width: 300px, 100%, 500px;
}
```

The rule above what say "never get smaller than 300 and never get bigger than 500 otherwise be 100% of parent width"

Clamp can also be applied to font size. Here is a [Fluid Typography](https://codepen.io/awdriggs/pen/jEbomaz) example that changes the font sizes based on the width of the page.

## Responsive Layouts
Putting together our new tools of media queries, responsive units and flexible sizes, we can begin to build fully responsive layouts.

A common practice is to start with mobile styling first. Why?
- Your small screen styles are in your base CSS and then as the screen gets larger, you add new rules or override old rules.
- Start Simple, your mobile site should be the most simple to navigate and read. 
- You create more rules as screen size increases, you don't have to replace rules for smaller devices.

There are some common patterns the people follow. [Here](https://medium.com/@daniaherrera/responsive-design-layout-patterns-70e710551818) is a good primer. An here is an [exhaustive collection](https://bradfrost.github.io/this-is-responsive/patterns.html)! 

### Two Example to Explore
I've made two simple examples for exploration. There is a live link and code for both.

#1 - Basic Column Shift 
- [demo](./tutorials/responsive-web/examples/layout/) 
- [html](./tutorials/responsive-web/examples/layout/index.html)
- [css](./tutorials/responsive-web/examples/layout/style.css)

#2 - Fluid Layout using CSS Grid 
- [demo](./tutorials/responsive-web/examples/layout-fluid/) 
- [html](./tutorials/responsive-web/examples/layout-fluid/index.html)
- [css](./tutorials/responsive-web/examples/layout-fluid/style.css)

Flexbox lends itself really well to responsive design. You can switch your flex items from columns to rows among other things. 

CSS Grid is really powerful and great for responsive design and deserves a tutorials on its own. I've linked to some resources below.

### Resources
- [slides](./slides.pdf)
- [recording]()
- [fonts](https://css-tricks.com/accessible-font-sizing-explained/#aa-avoid-setting-a-base-font-size)
- [clamp](https://css-tricks.com/linearly-scale-font-size-with-css-clamp-based-on-the-viewport/)
- [List of Responsive Design Patterns](https://bradfrost.github.io/this-is-responsive/patterns.html)
- [Responsive Design with Flexbox](https://www.w3schools.com/css/css3_flexbox_responsive.asp)
- [Interactive Guide to Grid](https://www.joshwcomeau.com/css/interactive-guide-to-grid/)
