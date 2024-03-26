---
title: "March 2024"
date: 2024-03-26T01:59:24+13:00
showDate: true
description: ""
showDescription: false
edit: false
archive: false
archiveNote: ""
draft: true
tags: [
    "rant-and-ramble", 
    "site/update", 
    ]
---

Since <span class="small-caps">someone</span> recently accused me of "*lying to my followers/subscribers*" for not having written a post since the PSA in February[^1], I'd like to set the record straight and confirm that I am indeed a blatant liar;

*I have been lying about writing in general since this site has been up.*

However, I haven't been twiddling my thumbs and doing nothing.

For the last month, I have been procrastinating writing by doing the other thing I said I was going to for the last two years: **updating my site's theme**, customising some styling, and learning how Hugo works so I can customise its structure and elements.

This article was originally going to be fun. I was going to show all the nice (imo) styling changes I made that you'll likely look at but never pay too much attention to.

*This is now a rant.*

In deference to the designer/developer of the theme I am using, they have made a very nice looking theme[^2] and I very much appreciate their hard work over the years at maintaining and adding features to it. In their defence, Hugo[^3] receives continuous updates and every time I spin it up, I find new features to learn about or changes to be aware of, so issues are to be expected.

In *my* defence, I am not a web developer nor am I an engineer, and to some extent I am barely a developer at all. Perhaps I am to blame for all the troubles I ran into because I didn't update the theme for six years and a lot can change in six years[^4].

<!-- *However*, the structure of the Go/Hugo, templates and styling code just astounds me. There are important variables which certain pieces of code depend on to function properly that are present *only* in the code and have **no definition**, which breaks a bunch of the touted features of the theme. -->

However, the structure, logic and organisation of a lot of the theme code just astounds me; they don't seem to reflect good coding practices at all. In fact, there are some important variables required for certain touted theme features to work which are present *only* in the code and have **no definition**, thus the features don't work out of the box. The majority of the styling code is focused on the `<article>` element and some attributes, such as the font, are defined redundantly in multiple places.

One major change between my version of the theme and the latest two year old version of the theme is its underlying HTML structure. The underlying structure of web pages in my version of the theme is essentially a bunch of `<div>` elements. The issue with relying solely on `<div>` elements is that they have no semantic meaning in HTML, i.e. something wrapped inside a `<div>` doesn't tell you much about what it is or what it's for[^5]. And that is a big accessibility problem (especially for screen-readers). The newest version uses better and more proper HTML elements like `<main>`, `<article>`, `<header>`, `<footer>` that are better for accessibility.

One unexpected outcome of upgrading the theme was that the styling of various elements changed: the spacing between lines, the opacity of the text; and I had to figure how they changed and how to change them back. I won't complain about that, it was a good learning experience.

However, there were also downsides. For smaller screen sizes, the underlines on the links on my homepage wouldn't wrap because of how they were implemented. It turns out that these nicely spaced underlines on my site are implemented as bottom borders. It also turned out that the links were being treated as `block` elements instead of `inline` elements because they were not wrapped in anything.

*What does this mean?* It means that since the link was a block, it wasn't as wide as its text was, it was **as wide as the entire page**, and because the "underline" was a bottom border for the block and not the text, it was also as wide as the entire page.

For the longest time, I wanted to have at least the option to change the font my site used but there was no easy way to do so because the theme hardcoded the font into the CSS and the Google fonts script, and there was no way to use Hugo variables in CSS so it would've been hardcoded one way or another. Recently however they added the feature to use Hugo variables in CSS. I figured out how to do it and I changed the code font to Sometype Mono.

You know how I talked about hidden variables above? Well, I ran into those trying to get the [gallery][3] to work. The gallery code relied on an option that didn't exist in the config file and so the site wouldn't build when I tried to use the gallery. One related problem, which is not the developer's fault, is that somewhere along the line, `.` in Hugo refers only to the current context, i.e. the page, and not to the site as a whole, and so a bunch of the logic in the gallery code simply didn't work because they referred to options that didn't exist.

The most recent problem that I ran into is related to how Hugo parses SASS. Any web person knows that CSS styles your website. Well, what if you want to use say, a colour, across multiple elements, or a perhaps particular font? You gotta write it out everywhere you want to use it. SASS is a pre-processor[^6] for CSS that lets you group similar styles together, define variables so you can reuse things (the colour or font above), and more. As a quick introduction, Hugo used to use one sass compiler and now prefers another one.

In the template code for my theme, it does something weird. If it's running locally as a development server, it builds fine. If it's not, it can't process the SASS into CSS. Why? It depends on some `npm` tools and I don't have `npm` or said tools installed. Like I said, I'm not a web developer. That's my problem, I know, but the catch is that it used to build perfectly fine without having to install *any* web (or additional) packages. And I don't want to use web packages. But what's the solution? I can use Dart Sass. On macOS, I can easily install it with Homebrew (which I also used to install Hugo), and I don't have to worry about `npm` and the gazillion dependencies it's bound to pull in. So, I edited the templates.

I know, I know. I've spent this whole post complaining. That's because this whole experience has been incredibly frustrating. But I promise it'll be over soon. I hope you've been noticing a trend here. I've had to edit *a lot* of stuff, a lot of the templates and code for this theme. In fact, I would go as far to say, I've kinda had to rewrite this entire theme. Which kinda defeats the purpose of using a theme in the first place. <!-- Now sure, often things are set in stone in a theme but I didn't expect to run into some of the issues I ran into.--> You expect themes to just work. And this doesn't.

Which is disappointing.

On a more positive note, I am going to continue modifying and essentially rewriting this theme. I really want to rewrite the SASS because it is simply structured poorly. I also want to implement some features I genuinely couldn't (this time around) since I had to fix a bunch of things, and they include:

- a return to top button for longer posts
- a nicely styled table of contents
- a way to embed "subset galleries" into posts
- make the [posts](/posts) page nicer than just a list with dates

As I said at the beginning, I was going to show you some nice but un-noteworthy styling changes I made. That will have to wait for another time. I am certain there are a lot more style changes I am going to make. And I'll tell you about them all together.

I thank whoever read this entire post and I thank anyone who read even part of it.

See you next time~~!

[^1]: the last post\: ["PSA: dated Feb. 2024"](../psa-february-2024)
[^2]: Sam is the name of the theme that I'm using.
[^3]: Hugo is the static site generator that I use to build this site: what that means is that essentially what you see on my site is what you get, there is no magic that dynamically loads new content or media.
[^4]: technically four years since the theme stopped getting updated in 2022.
[^5]: Here's a list of resources that I "consulted": [_Stop using so many divs! An intro into semantic HTML_][1] and [_Improving accessibility with div and span_][2]
[^6]: essentially it makes writing CSS easier and gets translated into proper CSS down the line.

[1]: https://dev.to/kenbellows/stop-using-so-many-divs-an-intro-to-semantic-html-3i9i
[2]: https://blog.segunolalive.com/posts/improving-accessibility-with-div-and-span/
[3]: /gallery
