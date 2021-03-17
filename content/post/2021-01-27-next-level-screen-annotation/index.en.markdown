---
draft: false
title: Next-Level In-Class Screen Annotation
author: Ryan Straight
date: '2021-03-16'
slug: next-level-screen-annotation
categories:
  - Teaching
tags:
  - "covid-19"
  - edtech
  - innovation
  - mobile learning
  - remote work
  - teaching
  - xaringan
  - xaringanExtra
subtitle: ''
summary: 'Using a *drawing monitor* and `xaringanExtra` for online teaching.'
authors: []
lastmod: '2021-03-16T20:35:04-07:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

<link href="{{< blogdown/postref >}}index.en_files/applause-button/applause-button.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index.en_files/applause-button/applause-button.js"></script>

<applause-button style="width: 50px; height: 50px;font-size:14px;&#10;         margin:30px 20px 20px 20px;&#10;         float:left;" color="#4682b4"></applause-button>

<blockquote style="font-size: 1.0em;color:#4682b4;padding-left:85px;">
If you found this useful, how about a round of applause?
</blockquote>

------------------------------------------------------------------------

Remote teaching during the SARS-CoV2 pandemic isn’t much different from what I normally do, insofar as I’m still teaching from my home office to students that (mostly) were planning on being online, regardless.

I’d been wondering what I can do to improve my engagement with the on-screen content during live class sessions. Like many, I’m using Zoom (which I’ve talked about in terms of \[using OBS to spice up your Zoom calls\]({{&lt; ref “post/2020-03-14-zoom-and-obs/index.md” &gt;}})) and, while I think the annotation tools provided are *decent* if a little clunky, I can’t bear trying to “write” on a screen using a mouse.

## The Drawing Monitor

Luckily, digital artists have sussed out this problem ages ago when the drawing tablets like the Wacom came out.

(This <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="rfa" style="height:0.75em;fill:Sienna;position:relative;"><path d="M413.1 222.5l22.2 22.2c9.4 9.4 9.4 24.6 0 33.9L241 473c-9.4 9.4-24.6 9.4-33.9 0L12.7 278.6c-9.4-9.4-9.4-24.6 0-33.9l22.2-22.2c9.5-9.5 25-9.3 34.3.4L184 343.4V56c0-13.3 10.7-24 24-24h32c13.3 0 24 10.7 24 24v287.4l114.8-120.5c9.3-9.8 24.8-10 34.3-.4z"/></svg> is not a drawing monitor; this <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="rfa" style="height:0.75em;fill:Sienna;position:relative;"><path d="M413.1 222.5l22.2 22.2c9.4 9.4 9.4 24.6 0 33.9L241 473c-9.4 9.4-24.6 9.4-33.9 0L12.7 278.6c-9.4-9.4-9.4-24.6 0-33.9l22.2-22.2c9.5-9.5 25-9.3 34.3.4L184 343.4V56c0-13.3 10.7-24 24-24h32c13.3 0 24 10.7 24 24v287.4l114.8-120.5c9.3-9.8 24.8-10 34.3-.4z"/></svg> is a drawing tablet. )

[![Drawing tablets have been around for a while](https://www.bhphotovideo.com/images/images2500x2500/wacom_pth451_intuos_pro_professional_pen_1002452.jpg)](https://www.bhphotovideo.com/c/replacement_for/1002452-REG/wacom_pth451_intuos_pro_professional_pen.html)

And these are great for particular things but (and I tried it) manipulating the Zoom annotation tools is not one of them.

Enter the drawing *monitor*: think of it as a combination of the drawing tablet (above) and a touch screen. So you can do this kind of thing (*this* <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="rfa" style="height:0.75em;fill:Sienna;position:relative;"><path d="M413.1 222.5l22.2 22.2c9.4 9.4 9.4 24.6 0 33.9L241 473c-9.4 9.4-24.6 9.4-33.9 0L12.7 278.6c-9.4-9.4-9.4-24.6 0-33.9l22.2-22.2c9.5-9.5 25-9.3 34.3.4L184 343.4V56c0-13.3 10.7-24 24-24h32c13.3 0 24 10.7 24 24v287.4l114.8-120.5c9.3-9.8 24.8-10 34.3-.4z"/></svg> is a drawing monitor):

[![Now you can actually see what you’re drawing.](https://media.giphy.com/media/lWdulVJxM5iDP9C4lg/giphy.gif)](https://gph.is/g/aQq2VBA)

Powerful for artists but why would it be of value for teaching online? Let’s talk about that.

## Application

What’s it great for? How about:

-   Code highlighting or debugging
-   Emphasizing and analyzing data visualization
-   Doing traditional paper markup
-   Demonstrating image manipulation
-   Using browser-based slide deck and a blank New Tab gives you an on-demand whiteboard without having to switch between screen shares
-   Compared to an iPad, this is one less device, login, et cetera, to have to worry about. *It’s just another monitor*.

That said, it struck me how janky the whole process was. Switching the annotation on and off, finding the button to change from pencil back to mouse, having to clear the annotations before moving on. It was really frustrating. Why not just have some keyboard shortcuts to do these things? One hand on the keyboard, one hand holding the pen, and you’re good to go.

## Wish list

So I tweeted about the lack of annotation-specific keyboard shortcuts and whoever runs the Zoom Twitter account actually replied, which was unexpected:

{{% tweet "1351910821325123592" %}}

Which I did. Who knows what will come of that. 🤷

*But wait!*

## Enter `xaringanExtra`’s *scribble* option

I’ve talked about it before but just as a little refresher: for my slide decks, I use an RMarkdown package called [`xaringan`](https://github.com/yihui/xaringan) by [Yihui Xie](https://yihui.org/), a software engineer at [RStudio](https://rstudio.com). (Remember, this site is build with [`blogdown`](https://bookdown.org/yihui/blogdown/), another RMarkdown package.) Everything is written in plain text and is human-readable (it’s just a version of Markdown) and incorporates R code natively. It allows you to easily do all the neat stuff you see around here.

Xaringan slide decks are so useful for a variety of reasons, one of which is their extensibility. One manifestation of that is the [`xaringanExtra`](https://pkg.garrickadenbuie.com/xaringanExtra/#/) package by [Garrick Aden-Buie](https://garrickadenbuie.com/), who is also with RStudio. Want an audio signal when your slides change. Try `use_slide_tone()`. Want to add a logo to all your slides? `use_logo()` to the rescue. Make your slides editiable? `use_editable()`! [The list goes on](https://pkg.garrickadenbuie.com/xaringanExtra/#/README?id=xaringanextra).

Check this out: how’s this for simple but super effective on-screen annotation?

<iframe src="https://pkg.garrickadenbuie.com/xaringanExtra/scribble/" width="100%" height="400px">
</iframe>

This is the demo for the *scribble* function in a Xaringan slide deck. Either click the <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512" class="rfa" style="height:0.75em;fill:Sienna;position:relative;"><path d="M497.9 142.1l-46.1 46.1c-4.7 4.7-12.3 4.7-17 0l-111-111c-4.7-4.7-4.7-12.3 0-17l46.1-46.1c18.7-18.7 49.1-18.7 67.9 0l60.1 60.1c18.8 18.7 18.8 49.1 0 67.9zM284.2 99.8L21.6 362.4.4 483.9c-2.9 16.4 11.4 30.6 27.8 27.8l121.5-21.3 262.6-262.6c4.7-4.7 4.7-12.3 0-17l-111-111c-4.8-4.7-12.4-4.7-17.1 0zM124.1 339.9c-5.5-5.5-5.5-14.3 0-19.8l154-154c5.5-5.5 14.3-5.5 19.8 0s5.5 14.3 0 19.8l-154 154c-5.5 5.5-14.3 5.5-19.8 0zM88 424h48v36.3l-64.5 11.3-31.1-31.1L51.7 376H88v48z"/></svg> or the `s` key on your keyboard while using the slide deck. Try flipping between slides. See how the annotations stay *only on the slide you scribbled on*? That’s a huge improvement on using Zoom to annotate over a slide and then having those scribbles carry on into the next slide.

And big shout-out to [Matt Warkentin](https://github.com/mattwarkentin) for [“doing the heavy lifting”](https://twitter.com/grrrck/status/1371872765054230534) to get scribble to work!

I got to use that particular package last night for the first time in class and I can’t begin to express how smooth and easy it made the process. Simply the ability to switch back and forth between slides that *maintained their respective annotations* was a game-changer. You often don’t realize just how much effort you’re putting forth trying to make something work until it works without friction.

So, if you’re teaching or presenting online and you want to annotate a slide deck, give **scribble** a try.
