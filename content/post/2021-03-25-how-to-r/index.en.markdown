---
draft: false
title: How to R
author: Ryan Straight
date: '2021-03-24'
slug: how-to-r
categories:
  - Code
tags:
  - R
  - RStats
  - RMarkdown
  - "how-to"
subtitle: ''
summary: 'I use `R` a lot. This is my collection of how-tos, tricks, and favorite bits.'
authors: []
lastmod: '2021-03-24T20:35:04-07:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
bibliography: ["example.bib"]
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

{{% toc %}}

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

## [formatR](https://yihui.org/formatr/)

A great way to keep your code looking tidy. Remember: space is your friend! The example Yihui Xie uses on his website is this poorly organized code:

``` r
## comments are retained;
# a comment block will be reflowed if it contains long comments;
#' roxygen comments will not be wrapped in any case
1+1

if(TRUE){
x=1  # inline comments
}else{
x=2;print('Oh no... ask the right bracket to go away!')}
1*3 # one space before this comment will become two!
2+2+2    # only 'single quotes' are allowed in comments

lm(y~x1+x2, data=data.frame(y=rnorm(100),x1=rnorm(100),x2=rnorm(100)))  ### a linear model
1+1+1+1+1+1+1+1+1+1+1+1+1+1+1+1+1+1+1+1+1+1+1  # comment after a long line
## here is a long long long long long long long long long long long long long comment that may be wrapped
```

And then, after using `formatR`:

``` r
## comments are retained; a comment block will be
## reflowed if it contains long comments;
#' roxygen comments will not be wrapped in any case
1 + 1

if (TRUE) {
    x = 1  # inline comments
} else {
    x = 2
    print("Oh no... ask the right bracket to go away!")
}
1 * 3  # one space before this comment will become two!
2 + 2 + 2  # only 'single quotes' are allowed in comments

lm(y ~ x1 + x2, data = data.frame(y = rnorm(100), x1 = rnorm(100), 
    x2 = rnorm(100)))  ### a linear model
1 + 1 + 1 + 1 + 1 + 1 + 1 + 1 + 1 + 1 + 1 + 1 + 1 + 
    1 + 1 + 1 + 1 + 1 + 1 + 1 + 1 + 1 + 1  # comment after a long line
## here is a long long long long long long long long
## long long long long long comment that may be
## wrapped
```

## Knitr

There’s so much that `knitr` can do and I find myself having to over and over research just how to do something. No more!

Including an image:

    knitr::include_graphics("image.ext")

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

Best to use the `icon` package for static icons.

## Project management: `ProjectTemplate`

Project management has always been my downfall in terms of finding the solution that works just the way I want it to. (And, yes, I know that *perfect* is the enemy of *good* but I have to procrastinate somehow, don’t I?) I really like `ProjectTemplate`, though. I typically use the minimal version of the template and it helps keep me organized and on a standard workflow. It’s easy to put down and pick back up later, as well.

## Citation, `papaja`, and BetterBibTeX

I use Zotero and, since I do a lot of writing in APA format, I use the `papaja` package to make that easier. As such, I use BibTeX (unsurprisingly).

### Quick copy from Zotero

Took me a while to learn this but as my Zotero library has thousands of entries, I don’t always use the full library as a .bib file (for obvious reasons). As I’m also constantly adding new entries and I don’t want to have to export a .bib every time, the *Quick Copy* option is as I can easily throw a new BibTeX entry into a .bib file in RStudio.

You can change the *Quick Copy* formatting by going to `Edit` <i class="fas  fa-arrow-right "></i> `Preferences` <i class="fas  fa-arrow-right "></i> `Export` and changing the Default Format to *BetterBibTeX*. Voila, you can start using the citation key.

### Different in-text citation forms

While I love doing everything like this in plain text, I can never remember how the different in-text citations work. So here’s a cheatsheet. We’ll be using (Ash et al. 2017) as the example.

My YAML includes: `bibliography: ["example.bib"]`

Depending on what RMarkdown template/document you’re using, you can also change the bibliography style.

I have this BibTeX entry in the `.bib` file:

``` bibtex
@article{Ash2017,
  title = {Unit, Vibration, Tone: A Post-Phenomenological Method for Researching Digital Interfaces},
  author = {Ash, James and Anderson, Ben and Gordon, Rachel and Langley, Paul},
  year = {2017},
  pages = {147447401772655},
  issn = {1474-4740},
  doi = {10.1177/1474474017726556},
  abstract = {Digital interfaces, in the form of websites, mobile apps and other platforms, now mediate user experiences with a variety of economic, cultural and political services and products. To study these digital mediations, researchers have to date followed a range of methodological strategies including the modification of pre-existing qualitative research methods, such as content analysis, discourse analysis and semiotics, among many others, and an experimentation with new methods designed to make visible the operation of data aggregation, analytics and algorithms that are hidden from users. Building upon, while distinct from these strategies, the article sets out a post-phenomenological approach to studying interfaces, websites and apps that explicitly interrogates how they appear as objects. In doing so, the article provides a response to a problem that animates contemporary cultural geography: that new cultural objects are emerging which place in question the habits and practices of analysis that composed the `new' cultural geography. To do this, the paper develops the concepts of unit, vibration and tone to unpack interfaces as sets of entities that work together to shape the experiences and responses of users. As such, the article provides a methodological vocabulary for the analysis of how interfaces operate to modulate user response and action on a series of habitual and un-reflected upon levels and thereby to create outcomes that suit their owners and operators.},
  file = {D\:\\Sync\\Work\\School\\Articles\\Cultural Geographies\\Ash et al\\Ash et al. - 2017 - Unit, vibration, tone a post-phenomenological method for researching digital interfaces.pdf},
  journal = {Cultural Geographies},
  keywords = {digital geographies,digital methods,interfaces,materiality,post-phenomenology}
}
```

Obviously, the abstract is optional but I’m leaving here for demonstration purposes. For the different formats of in-text citation:

`[@Ash2017]` gives you what you saw above: (Ash et al. 2017)  
`[@Ash2017, pp. 22]` gives you: (Ash et al. 2017, 22)  
`[-@Ash2017]` removes the author: (2017)  
`@Ash2017` (without the brackets) gives you: Ash et al. (2017)  
`@Ash2017 [pp. 22]` gives you: Ash et al. (2017, 22).

If you wanted to include a citation in the bibliography but not actually cite it in the text, just add this to the YAML:

``` yaml
nocite: |
  @Ash2017
```

Finally, just place a `## References` header at the bottom of your file and voila, instant bibliography!

### `papaja`

For doing more nuanced work, I use the [`papaja`](https://github.com/crsh/papaja) package to create APA-formatted papers. I highly encourage folks–especially students that produce APA-formatted documents frequently–to check it out. It’s so handy.

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

Then, add this to your `custom.css` (or whatever custom CSS file you’re using) and alter to your liking:

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

In the text, this will appear as `` `r cor(x, y, method = c('pearson'))` ``.

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

## [`xaringanExtra`](https://pkg.garrickadenbuie.com/xaringanExtra/)

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

This stuff isn’t R-related, specifically, but makes working with R a lot easier. I’ll probably add to this as I think of things.

### [Copycat](https://chrome.google.com/webstore/detail/copycat/jdjbiojkklnaeoanimopafmnmhldejbg)

A Chrome extension that allows for quick copying of URLs, text, et cetera, as markdown syntax. When creating a list of links or resources, for example, this is very, very handy. It speeds things up considerably to just be able to copy and paste without thinking about the markdown syntax.

### Proper file naming

Follow the advice of [Jenny Bryan](https://jennybryan.org) and use filenames that are:

1.  machine readable
2.  human readable
3.  play well with default ordering

Her [classic slide deck](http://www2.stat.duke.edu/~rcs46/lectures_2015/01-markdown-git/slides/naming-slides/naming-slides.pdf) on the topic is a wealth of guidance. In short:

**Good**:  
2021-03-13\_blogpost\_how-to-r.Rmd  
2021-03-21\_blogpost\_stream-deck-for-online-teaching.Rmd  
2021-04-04\_blogpost\_something-i-may-write-who-knows.Rmd

Chronological order template:

`YYYY-MM-DD_Project-title_Specific-file_Version.ext`

Logical order:

    01_Filename-title-that-is-descriptive.ext
    02_Filename-title-that-is-descriptive.ext
    90_Filename-title-that-is-descriptive.ext

Function/value/variable naming:

`variable.name` **not** `variable_name`

**Bad**:  
draft How to R.Rmd  
New File (1)(1)(1).PDF  
image.jpg  
RS-here are my edits to yourfile.docx

Help Today-You be kind to Tomorrow-You by using proper naming!

------------------------------------------------------------------------

Eventually, I’ll do an entire post about my favorite RMarkdown templates for a variety of uses. Until then, hopefully this is helpful!

## References

<div id="refs" class="references csl-bib-body hanging-indent">

<div id="ref-Ash2017" class="csl-entry">

Ash, James, Ben Anderson, Rachel Gordon, and Paul Langley. 2017. “Unit, Vibration, Tone: A Post-Phenomenological Method for Researching Digital Interfaces.” *Cultural Geographies*, 147447401772655. <https://doi.org/10.1177/1474474017726556>.

</div>

</div>
