# What is the difference between classes and IDs in CSS?

What is an ID?

> In an HTML document, the CSS ID selector matches an element based on the value of its id attribute. The selected element's ID attribute must match exactly the value given in the selector.

What is a class?

> The CSS class selector matches elements based on the contents of their class attribute.

Given these descriptions, they are basically the same thing in practice but differentiated by their HTML attribute. As far as CSS is concerned, there is virtually no difference. If you have an ID selector or a CLASS selector, the styles will be applied the same. The one major difference is in regards to specificity.

To really get to the root of this question, I feel that the real question should be, "What is CSS specificity?".

CSS Specificity is a matrix calculation that determines in what specific order a CSS style will be applied to a DOM element. The lower the specificity rating, the more universally it will be applied to DOM elements and the easier it is to over-write. The higher the specificity, the more specifically the style will be applied to a DOM element and the harder it is to over-write.

You could think about it this way. The more specific you are about describing something, the higher the specificity rating. Think of it this way, if you are describing someone's house, would you say, "It's a house on a street"? No, you would give a better description of the house, if not directions and its address.

The following is a chart of specificity from the W3C, 6.4.3 Calculating a selector's specificity.

```css
 *              {}  /* a=0 b=0 c=0 d=0 -> specificity = 0,0,0,0 */
 li             {}  /* a=0 b=0 c=0 d=1 -> specificity = 0,0,0,1 */
 li:first-line  {}  /* a=0 b=0 c=0 d=2 -> specificity = 0,0,0,2 */
 ul li          {}  /* a=0 b=0 c=0 d=2 -> specificity = 0,0,0,2 */
 ul ol+li       {}  /* a=0 b=0 c=0 d=3 -> specificity = 0,0,0,3 */
 h1 + *[rel=up] {}  /* a=0 b=0 c=1 d=1 -> specificity = 0,0,1,1 */
 ul ol li.red   {}  /* a=0 b=0 c=1 d=3 -> specificity = 0,0,1,3 */
 li.red.level   {}  /* a=0 b=0 c=2 d=1 -> specificity = 0,0,2,1 */
 #x34y          {}  /* a=0 b=1 c=0 d=0 -> specificity = 0,1,0,0 */
 style=""           /* a=1 b=0 c=0 d=0 -> specificity = 1,0,0,0 */
```

For an interactive guide to specificity, check out this [Specificity Calculator](https://specificity.keegan.st/).

Buyer beware. Use specificity as a tool of intent and not a hammer. Seasoned CSS developers will tell you that being overly specific with CSS selectors will cause you nothing but frustration as the project evolves. This is the reason behind such frameworks as OOCSS, SMACSS and BEM.

## Specificity and the cascade
The cascade in CSS is a very important thing to keep in mind, but simply following the cascade without consideration of specificity is a fool's game.

As the following code clearly shows, the cascade has a role to play, but specificity trumps all. In fact, when the cascade seems to mystify most developers, they typically resort to using specificity as a hammer. This is when many developers simply go into the HTML, wrap it in another `<div>` and add a new ID on that element.

<a class="jsbin-embed" href="http://jsbin.com/tanujo/embed?html,css,output">JS Bin on jsbin.com</a><script src="https://static.jsbin.com/js/embed.min.js?4.1.1"></script>

#### Specificity and Thor's hammer
How can you tell that a developer does not understand specificity or the cascade? Easy, look for code as illustrated in this bin. What is interesting to note is that the use of an ID alone is usually more than enough to have a really high specificity rating. But when developers follow the whole selector path to the ID, this use of hyper-specificity (jokingly called Thor's hammer) really causes issues down the road as the only way to combat this is to add even more specificity to the CSS selector and the more rules you add like this, the more complex the CSS, the higher risk for error and the longer it takes the CSSOM to render.

<a class="jsbin-embed" href="http://jsbin.com/jogidil/1/embed?html,css,output">JS Bin on jsbin.com</a><script src="https://static.jsbin.com/js/embed.min.js?4.1.1"></script>

## How is this different in HTML?

Aside from CSS differences, there are specific differences in regards to the HTML attributes and how the browser will render this content. That being said, HTML is very forgiving and will not throw a non-rendering error on the page if you break these rules. But, there will be issues that may arise.

Classes can be used again and again on the page and have relative specificity as determined by the matrix above. IDs on the other hand are to be unique and only referenced ONCE per view. Like I said, using an ID over and over in the same view will not break its UI. In fact the browser UI rendering engine will not really care and may throw a silent error. But when using JavaScript and you try to target an ID that is duplicated on a view, there will be a significant error that will break functionality.

## How I would answer this in an interview
To answer the CSS part of the question, I would reference the relative differences in specificity (but be sure you understand that, as it will probably be a follow-up question). Then I would also caveat that with the fact that IDs need to be unique per view and have a higher specificity rating, whereas CLASSES are less specific and are intended for repeated use.
