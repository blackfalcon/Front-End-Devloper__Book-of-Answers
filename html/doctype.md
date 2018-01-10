# What does a `doctype` do?

This is a pretty elementary question when it comes to web development, and anyone asking this is someone who likes to revel in the historical records of web development. It is one of those questions that will trip up most people as it is something that most rarely ever think about anymore, especially when we are shoulders deep inside learning the latest trends in JavaScript or CSS.

There is virtually no history on this question in the Github log, assuming history was lost when this project was moved to h5bp. That being said, I can only assume what the intent behind the question is.

The MDN glossary describes `doctype` as this.

> In HTML, the doctype is the required "<!DOCTYPE html>" preamble found at the top of all documents. Its sole purpose is to prevent a browser from switching into so-called “quirks mode” when rendering a document; that is, the "<!DOCTYPE html>" doctype ensures that the browser makes a best-effort attempt at following the relevant specifications, rather than using a different rendering mode that is incompatible with some specifications.

The `doctype` instruction is as old as the HyperText Markup Language itself and played a much more important role in the early days of the web then it does today. Specifically during the emerging days of XML, XHTML and the aforementioned “quirks mode”. With these emerging technologies and evolving standards in HTML, the required code used to be much more verbose.

##### XHTML 1.1
```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
```

##### HTML 4.01
There were numerous issues with all the work dine between the HTML 1.1 standard and the newer HTML 4.0 standard, especially regarding the use of XML strictness. Finally, the committees settled on what became HTML 4.1 and the famed `transitional` statement that allowed for developers to NOT have to be overly governed by the strictness of XML standards.

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
```

##### HTML 5
With all the drama surrounding the HTML 4.1 standard, the huge movements in the community wanted to do away with all this verbosity and settled on what we have today, a simplified standard that was adopted by all browser manufacturers.

```html
<!DOCTYPE html>
```

## What is “quirks mode”?

This question is rooted in history as `doctype` is. In regards to modern web development, it is meaningless. In regards to history, it has everything to do with the early days of the web. In the days of Netscape vs. Microsoft, each company was in the business of building browsers with non-standard implementations of the HTML spec. That being said, as the HTML standards movement gained favor, these browser manufacturers needed a way to allow for their browsers to adopt the new standards without breaking most of the web at that time.

## How I would answer this in an interview

`doctype` is a tool to enforce HTML standards use in the rendered document and avoid using any "quirks mode" rendering.

If asked, "What is 'quirks mode'?" as a follow-up, I'd respond with, "An outdated tool that tried to 'un-break' the old Internet."
