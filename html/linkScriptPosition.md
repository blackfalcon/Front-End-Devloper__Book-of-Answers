# Why is it generally a good idea to position CSS `<link>`s between `<head></head>` and JS `<script>`s just before `</body>`? Do you know any exceptions?

This is a really long question, so let's unpack what this is really asking. The following code example illustrates what this is eluding to.

```html
<!doctype html>
<html>
  <head>
    <link rel="stylesheet" href="main.css">
  </head>
  <body>

    <script src="main.js" async defer></script>
  </body>
</html>
```

Knowing this, why is it a good idea to put the CSS in the `<head>` element and then the JavaScript in the `<body>` tag? The answer is pretty simple, it has everything to do with performance and order of events.

When the browser receives the HTML document, it immediately starts to fire off a series of events. The HTML is converted into a series of nodes and creates the DOM. At the same time, all the external resources are being called and loaded into memory as well. In regards to the CSS, you can really load this at any time in the HTML/DOM, but most likely, you want all the CSS loaded into the CSSOM by the time the DOM is created and you reach the browser's first meaningful paint.

Within the targets .5 second that it takes to do this, the user is highly unlikely to interact with the page, so loading the JavaScript first has the drawback of potentially slowing down this process as the browser needs to request the JS and process into the browser's memory. This is considered a blocking event as the browser will not render the rest of the page until the JavaScript has completed.

There is a secondary benefit from putting the JavaScript at the end of the document and that is a preferred order of events. JavaScript requires that the DOM is ready in order to work. In the old days, we had to wrap out JavaScript with a `document.ready()` function. This process is to load the JavaScript at the head of the document, wait for it to load, then the browser can create the DOM, all the while the JavaScript is sitting there waiting until the document is ready.

By putting it at the bottom, the HTML document has loaded and within the split second that the browser requests the JavaScript and processes it, the DOM and the CSSOM are complete and the JavaScript can execute all its commands.

### Exceptions

Now there are some exceptions to this architecture. One example is when using the modernizr library. The intent of this tool is to test the browser of its features prior to the rendering of the DOM and the CSSOM. Running this series of tests after the DOM and CSSOM are created renders this tool useless.

This is but one example, but there will be times when the JavaScript needs to load first, but most of the time it's ok to load it at the end.

## How I would answer this in an interview

The short answer to this question is simply, performance. Exceptions are limited to JavaScript utilities that are needed to run prior to the rendering of the DOM.
