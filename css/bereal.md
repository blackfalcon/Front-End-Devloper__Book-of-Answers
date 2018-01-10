# Let's be real here ...

In reading more and more of these questions, I am finding some questions where there is some historical significance or relative importance to the overall community, but knowing the answers to these colloquial questions does not, in any way, establish your personal creditability or skill level as a front-end developer.

I would also argue that some of these questions should be removed from this list altogether. So, if interested, read on. If not, ignore and get onto the more important things in life.

#### Describe BFC(Block Formatting Context) and how it works.
Why is this question here? This is some really nerdy crap in regards to how the view is laid out. Questions like `Describe Floats and how they work.` and `What are the various clearing techniques and which is appropriate for what context?` are somewhat more important, but even those are seriously outdated techniques.

If you are leading an interview and ask someone to describe BFC, IMHO, you suck at interviewing.

#### Explain CSS sprites, and how you would implement them on a page or site.
No. No. No. CSS sprites are old and krusty, SVG sprites are the new hotness.

This is an outdated technique and should never be asked in an interview. Even if your app uses sprites, don't ask this question. Don't put someone in a position to have to explain an out-dated technique that they may not even know and make the interview awkward.

#### What are your favourite image replacement techniques and which do you use when?
I am logging this question under the section of "why even ask this?" because it is, once again, more of historical significance versus actual current practice. The art of image replacement was very popular before the days of SVG and icon web-font use. If I were asked this question, I would reply with, "I don't, I use SVGs." Me personally, I stopped paying attention to this around 2012.

But, if you want a walk down memory lane, here is a complete [history](https://css-tricks.com/the-image-replacement-museum/) of the technique.

#### How do you serve your pages for feature-constrained browsers?
There is no discussion here. CSS feature detection is done with [Modernizr](https://webdesign.tutsplus.com/tutorials/css-feature-detection-modernizr-or-feature-queries--cms-23508). End of story.

While this tool is useful and is still supported, its usefulness is waning. Modernizr had its hay-day in the early days of CSS3 when developers had to fight issues with legacy versions of IE. The good news is, we don't have as many issues as we used to. With tools like this and [caniuse](https://caniuse.com/), we have shown a bright light on the issues front-end developers face and browser developers have done a great job responding to these issues. In fact, when I was last teaching UI dev, I just removed this section as it's not that relevant and there are more important things to learn.

If I were interviewing a new UI developer, and depending on their background and development history, if they never had to deal with this at any scale, I would not consider this an issue.

#### How do you optimize your web pages for print?
The use of print stylesheets has really gone down over the years. Browsers have gotten better at rendering content to be printed, not to mention, the vast majority of content displayed on mobile devices will never be printed. While this is a technique that may have some use, expecting a front-end developer to know this off-hand today is pretty lame if you ask me. There are WAY more important things to worry about.

That all being said, `@media print {}` is your golden ticket. If you need to do this, please read [How To Set Up A Print Style Sheet](https://www.smashingmagazine.com/2011/11/how-to-set-up-a-print-style-sheet/), a great article from 2011 that will help you out.

#### List as many values for the display property that you can remember.
How can I say this ... this is a DUMB QUESTION! Why? I have been doing front-end development for over 12 years now and I can only rattle off 4 or 5 off the top of my head. There are only really 3 or 4 I EVER use, and when I can't remember, that is what MDN docs are for. Isn't it more important that I know that this CSS property even exists and I know how to use it versus listing off the different property types like I am a living CSS spec machine?

If you care, here is the [list](https://developer.mozilla.org/en-US/docs/Web/CSS/display)

#### The 'C' in CSS stands for Cascading. How is priority determined in assigning styles (a few examples)? How can you use this system to your advantage?
This is a follow-up question to the [What is the difference between classes and IDs in CSS?](css/idvsclass.md) question. This again is really a question about specificity and the order in which the CSS is written in the stylesheet.

The question, `How can you use this system to your advantage?` I am particularly uncomfortable with. The answer to this is to use specificity as a hammer to combat the natural flow of the cascade, and as discussed, this is a BAD thing in most cases.
