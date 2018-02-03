# Follow Along Link Highlighting

A page built to practice manipulating styles with `getBoundingClientRect()`. Built for Wes Bos' [JavaScript 30](https://javascript30.com/) course.

[![Screenshot of Follow Along Link Highlighting page](https://res.cloudinary.com/gerhynes/image/upload/v1517522018/Screenshot-2018-2-1_Follow_Along_Nav_zfrlub.png)](https://gk-hynes.github.io/follow-along-link-highlighting/)

## Notes

This is practice for replicating Stripe's dropdown menus. This project involves creating a highlight so that when you highlight over something it will figure out the width, height, and location on the page of that element.

First select all the links on the page.

Then create a span with a class of `highlight`.

```js
const highlight = document.createElement("span");
highlight.classList.add("highlight");
document.body.append(highlight);
```

Make a function, `highlightLink`, and listen for the `mouseenter` event on all links.

Inside `highlightLink`, call the `getBoundingClientRect` method on the triggers, i.e. the links.

```js
const linkCoords = this.getBoundingClientRect();
```

`getBoundingClientRect` give you all of the information about where on the page a particulaer element exists.

Next, set the width and height of the highlight to be equal to the width and height of the link coordinates.

Because highlight has a property of `transition: all 0.2;` it will grow and shrink over .2 seconds rather than snapping immediately.

Take the highlight and apply a `transform` style of `translate(${coords.left}px, ${coords.top}px);`

The highlighting now works, _but_ if you have scrolled the highlight will be off by the amount you have scrolled down.

To remedy this, take how far the person has scrolled down and add that.

```js
const coords = {
  width: linkCoords.width,
  height: linkCoords.height,
  top: linkCoords.top + window.scrollY,
  left: linkCoords.left + window.scrollX
};
```
