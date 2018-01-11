# Let's be real here ...

In reading more and more of these questions, I am finding some questions where there is some historical significance or relative importance to the overall community, but knowing the answers to these colloquial questions does not, in any way, establish your personal creditability or skill level as a front-end developer.

I would also argue that some of these questions should be removed from this list altogether. So, if interested, read on. If not, ignore and get onto the more important things in life.

#### Describe BFC(Block Formatting Context) and how it works.
Why is this question here? This is some really nerdy crap in regards to how the view is laid out. Questions like `Describe Floats and how they work.` and `What are the various clearing techniques and which is appropriate for what context?` are somewhat more important, but even those are seriously outdated techniques.

If you are leading an interview and ask someone to describe BFC, IMHO, you suck at interviewing.

#### How do you serve your pages for feature-constrained browsers?
There is no discussion here. CSS feature detection is done with [Modernizr](https://webdesign.tutsplus.com/tutorials/css-feature-detection-modernizr-or-feature-queries--cms-23508). End of story.

While this tool is useful and is still supported, its usefulness is waning. Modernizr had its hay-day in the early days of CSS3 when developers had to fight issues with legacy versions of IE. The good news is, we don't have as many issues as we used to. With tools like this and [caniuse](https://caniuse.com/), we have shown a bright light on the issues front-end developers face and browser developers have done a great job responding to these issues. In fact, when I was last teaching UI dev, I just removed this section as it's not that relevant and there are more important things to learn.

If I were interviewing a new UI developer, and depending on their background and development history, if they never had to deal with this at any scale, I would not consider this an issue.
