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

### Experiment 1
Open up this page and change the size of your browser window. What happens?
[Experiment 1 Link](.examples/queries/index.html)

This is all done through CSS media queries. These are blocks of CSS that get triggered at certain page width.

```CSS
@media only screen and (min-width: 768px) {
  /* put any rules that you want to overwrite or add with the {} of this bloc */

  body {
    background-color: #f0c808;
  }
}
```

In play English the block of code above says "when the screens width is at least 768px wide, add these rules!"

You overwrite previously applied rules or apply new rules. You ONLY have to put in CSS declarations for what you want to change, don't repeat rules that aren't effected! 

## Responsive Unit 




## Flexible  Sizing
min/max units
percentages



## Resources
[fonts](https://css-tricks.com/accessible-font-sizing-explained/#aa-avoid-setting-a-base-font-size)
[clamp](https://css-tricks.com/linearly-scale-font-size-with-css-clamp-based-on-the-viewport/)
