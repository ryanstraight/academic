---
draft: TRUE
title: How to R
author: Ryan Straight
date: '2021-03-25'
slug: how-to-r
categories:
  - Code
tags:
  - R
  - RStats
  - RMarkdown
  - "how-to"
subtitle: ''
summary: 'I use `R` a lot. This is my collection of how-tos.'
authors: []
lastmod: '2021-03-18T20:35:04-07:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

<link href="{{< blogdown/postref >}}index.en_files/applause-button/applause-button.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index.en_files/applause-button/applause-button.js"></script>
<link href="{{< blogdown/postref >}}index.en_files/font-awesome-animation/font-awesome-animation-emi.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index.en_files/fontawesome/js/fontawesome-all.min.js"></script>

<link href="{{< blogdown/postref >}}index.en_files/font-awesome/css/fontawesome-all.min.css" rel="stylesheet" />
<link href="{{< blogdown/postref >}}index.en_files/font-awesome/css/fontawesome-all.min.css" rel="stylesheet" />

<applause-button style="width: 50px; height: 50px;font-size:14px;&#10;         margin:30px 20px 20px 20px;&#10;         float:left;" color="#4682b4"></applause-button>

<blockquote style="font-size: 1.0em;color:#4682b4;padding-left:85px;">
If you found this useful, how about a round of applause?
</blockquote>

------------------------------------------------------------------------

I forget how to do a lot in R when I only do it once every year or two. I also wanted a place to keep track of my favorite packages. So:

## Updating R with `installr`

This is probably the simplest one on the list. Per the `installr` vignette:

``` r
if(!require("installr")) install.packages('installr')
library("installr")
updateR() # this will open dialog boxes to take you through the steps.
# OR use:
# updateR(TRUE) # this will use common defaults and will be the safest/fastest option
```

You should run it in the Rgui, not in RStudio. And that’s it! 🥳

## Proper naming

Chronological order template:

`YYYY-MM-DD_Project-title_Specific-file_Version.ext`

Logical order:

    01_Filename-title-that-is-descriptive.ext
    02_Filename-title-that-is-descriptive.ext
    90_Filename-title-that-is-descriptive.ext

Function/value/variable naming:

`variable.name` **not** `variable_name`

## [formatR](https://yihui.org/formatr/)

A great way to keep your code looking tidy. Remember: space is your friend!

## Knitr

There’s so much that `knitr` can do and I find myself having to over and over research just how to do something. No more!

Including an image:

``` r
knitr::include_graphics("image.ext")
```

or

``` r
knitr::include_graphics("url")
```

## Installing and loading packages

I give Rmd files to my students to use and practice with. This makes sure they don’t run into issues with not having packages installed:

``` r
for (package in c('package1', 'package2', 'package3')) {
    if (!require(package, character.only=T, quietly=T)) {
        install.packages(package, repos="http://cran.us.r-project.org")
        library(package, character.only=T)
    }
}
```

## Including icons and animation

To use `FontAwesome`:

`fontawesome::fa("arrow-down", fill = "Sienna")`: <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="rfa" style="height:0.75em;fill:Sienna;position:relative;"><path d="M413.1 222.5l22.2 22.2c9.4 9.4 9.4 24.6 0 33.9L241 473c-9.4 9.4-24.6 9.4-33.9 0L12.7 278.6c-9.4-9.4-9.4-24.6 0-33.9l22.2-22.2c9.5-9.5 25-9.3 34.3.4L184 343.4V56c0-13.3 10.7-24 24-24h32c13.3 0 24 10.7 24 24v287.4l114.8-120.5c9.3-9.8 24.8-10 34.3-.4z"/></svg>

To use `emo::ji`:

`emo::ji("sweat_smile")`: 😅

To use [`anicon`](https://anicon.netlify.app/):

`anicon::nia("Some text!", animate="wrench")`: <span class=" faa-wrench animated " style=" display: -moz-inline-stack; display: inline-block; transform: rotate(0deg);">Some text!</span>

The only bummer about `anicon` and using it for FontAwesome icons is that it doesn’t play well in Blogdown in my experience. The text works great, though. Xaringan, either. Best to use the `icon` package for static icons.

## Project management: `ProjectTemplate`

Project management has always been my downfall in terms of finding the solution that works just the way I want it to. (And, yes, I know that *perfect* is the enemy of *good* but I have to procrastinate somehow, don’t I?) I really like `ProjectTemplate`, though. I typically use the minimal version of the template and it helps keep me organized and on a standard workflow. It’s easy to put down and pick back up later, as well.

## Citation, `papaja`, and BetterBibTeX

I use Zotero and, since I do a lot of writing in APA format, I use the `papaja` package to make that easier. As such, I use BibTeX (unsurprisingly).

### Quick copy from Zotero

Took me a while to learn this but as my Zotero library has thousands of entries, I don’t always use the full library as a .bib file (for obvious reasons). As I’m also constantly adding new entries and I don’t want to have to export a .bib every time, the *Quick Copy* option is as I can easily throw a new BibTeX entry into a .bib file in RStudio.

You can change the *Quick Copy* formatting by going to `Edit` <i class="fas  fa-arrow-right "></i> `Preferences` <i class="fas  fa-arrow-right "></i> `Export` and changing the Default Format to *BetterBibTeX*. Voila, you can start using the citation key.

### Different in-text citation forms

While I love doing everything like this in plain text, I can never remember how the different in-text citations work. So here’s a cheatsheet:

## All things [Xaringan: Presentation Ninja](https://github.com/yihui/xaringan)

I use the `xaringan` package a *lot*. I gave up Powerpoint years ago in favor of something that’s lightweight, can include native R calculations and code, and is mobile, accessible, and responsive.

There’s a whole section of [*R Markdown: The Definitive Guide*](https://bookdown.org/yihui/rmarkdown/xaringan.html) devoted to xaringan but here are thing little bits that I really love:

### Progress bar

Add the `slideNumberFormat` lines to your `YAML`.

``` r
output:
  xaringan::moon_reader:
    nature:
      slideNumberFormat: |
       <div class="progress-bar-container">
         <div class="progress-bar" style="width: calc(%current% / %total% * 100%);">
         </div>
       </div>
```

Then, add this to your `custom.css` and alter to your liking:

``` css
.remark-slide-number {
  position: inherit;
}

.remark-slide-number .progress-bar-container {
  position: absolute;
  bottom: 0;
  height: 4px;
  display: block;
  left: 0;
  right: 0;
}

.remark-slide-number .progress-bar {
  height: 100%;
  background-color: red;
}
```

This gives you a thin red progress bar at the bottom of each slide. Much better than numbered slides!

### Verbatim code

This allows you to put verbatim in-line R code anywhere in your presentation. You can also do this in RMarkdown, generally. Great for demonstrating just how the *entirety* of the code should be written, not just what’s wrapped in it.

``` r
`` `r cor(x, y, method = c('pearson'))` ``
```

### Start with a *Please Stand By* slide

Use this directly after your R setup code chunk:

``` r
background-image: url(https://media.giphy.com/media/CdhxVrdRN4YFi/giphy.gif)
background-position: center
background-color: #000
background-size: contain
```

This sets your very first slide full screen as:

![](https://media.giphy.com/media/CdhxVrdRN4YFi/giphy.gif)<!-- -->

## xaringanExtra

I recently wrote about using the `scribble()` function from `xaringanExtra`, which is orders of magnitude easier to use when annotating a slide deck and sharing via Zoom. Other functions from the package I really like:

``` r
# xaringanExtra options

# Includes a "subtle tone" when slides change. Good for accessibility
xaringanExtra::use_slide_tone() # turns on the audio tone when slides change

# Provides more obvious code highlighting. Great for teaching.
xaringanExtra::use_extra_styles(  # higlights code
  hover_code_line = TRUE,         #<<
  mute_unhighlighted_code = TRUE  #<<
)

# Turns on clipboard options. Great for giving code to students.
xaringanExtra::use_clipboard()    # turns on the clipboard option
htmltools::tagList(
  xaringanExtra::use_clipboard(
    button_text = "<i class=\"fa fa-clipboard\"></i>",
    success_text = "<i class=\"fa fa-check\" style=\"color: #90BE6D\"></i>",
    error_text = "<i class=\"fa fa-times-circle\" style=\"color: #F94144\"></i>"
  ),
  rmarkdown::html_dependency_font_awesome()
)

# The sainted scribble function I keep talking about.
xaringanExtra::use_scribble()     # turns on scribble, built-in annotation
```

## Supplemental

This stuff isn’t R-related, specifically, but makes working with R a lot easier.

### [Copycat](https://chrome.google.com/webstore/detail/copycat/jdjbiojkklnaeoanimopafmnmhldejbg)

A Chrome extension that allows for quick copying of URLs, text, et cetera, as markdown syntax.
