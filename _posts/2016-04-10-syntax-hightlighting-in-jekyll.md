---
layout: post
title:  "Syntax Highlighting in Jekyll on Github Pages"
date:   2016-04-10 23:17:39 -0800
categories: jekyll
excerpt: "How I prettified the syntax-highlighting on my Jekyll blog hosted on GitHub Pages."
---

![Before and After]({{ site.baseurl }}/assets/images/syntax.png)

I was having a heck of a time getting my syntax highlighting to work in this new Jekyll bog. I don't like the standard colors
for the syntax-highlighting. Can you say DULL? I just wanted the syntax highlighting to go from boring to interesting, but I had a lot of trouble finding solutions that worked for me.

There are **lots** of blog posts
and Stack Overflow entries that talk about how to customize or improve syntax highlighting in markdown, but many of them are old and don't apply anymore,
or they involve extra plugins or things that don't work on GitHub Pages, like Pygments. I'm not really savvy with CSS (yet), so I didn't realize that the major problem was some CSS that was conflicting with the syntax highlighting. Spent a lot of time spinning my wheels on that. ⏳

 I finally got it to work to my satisfaction (at least for now), so I thought I'd put this out there if it can help someone else. This is probably not an ideal solution, but it works for me.

### Here is what I did 👏

I started with a syntax-highlighting css file using the [solarized-light color palette][solarized] that I found [here][css-file]. Thank you Dmitri Moore.

I made a few other changes to it to more closely match what is in Jekyll's default `_sass/_syntax-highlighting.scss` file. I made some more changes so I like the look of my favorite language, Python.

Then, I added this code from `_sass/_base.scss`, changing the `background-color` for the `code` inside the `pre` to match the `background-color` of the solarized-light color palette.

~~~scss
// override the _base.scss
pre,
code {
    font-size: 15px;
    border: 1px solid $grey-color-light;
    border-radius: 3px;
    background-color: #fdf6e3;
}

code {
    padding: 1px 5px;
}
~~~

This file is now the `_sass/_syntax-highlighting.scss` file. You can find the file in the [source on Github.][purplediane]

In my `_config.yml` file, I left the `markdown: kramdown` as it is and ended up not needing to change anything else. Some places recommended adding `highlighter: rouge`, but I didn't see that it made any difference. Perhaps later I will find a reason to use it.

In my markdown files, I use the "Github-style" fenced code blocks of `~~~language` rather than the *Liquid* commands.

I freely admit I had only a vague idea of what I'm doing here. 😁 If you have a comment or suggestion, and I haven't yet managed to turn on comments here, you can always message me via Twitter.


[css-file]: http://demisx.github.io/jekyll/2014/01/13/improve-code-highlighting-in-jekyll.html
[solarized]: http://ethanschoonover.com/solarized
[purplediane]: https://github.com/purplediane/purplediane.github.io/blob/master/_sass/_syntax-highlighting.scss
