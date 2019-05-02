---
layout: post
title: "Inblogural Post, Web Logging my PhD"
comments: true
date: 2019-05-02
---
<!-- Styles -->
<style>
.example1 {
 height: 50px;
 overflow: hidden;
 position: relative;
}
.example1 h3 {
 font-size: 3em;
 color: limegreen;
 position: absolute;
 width: 100%;
 height: 100%;
 margin: 0;
 line-height: 50px;
 text-align: center;
 /* Starting position */
 -moz-transform:translateX(100%);
 -webkit-transform:translateX(100%);
 transform:translateX(100%);
 /* Apply animation to this element */
 -moz-animation: example1 15s linear infinite;
 -webkit-animation: example1 15s linear infinite;
 animation: example1 15s linear infinite;
}
/* Move it (define the animation) */
@-moz-keyframes example1 {
 0%   { -moz-transform: translateX(-100%);  }
 100% { -moz-transform: translateX(100%); }
}
@-webkit-keyframes example1 {
 0%   { -webkit-transform: translateX(-100%); }
 100% { -webkit-transform: translateX(100%); }
}
@keyframes example1 {
 0%   {
 -moz-transform: translateX(-100%); /* Firefox bug fix */
 -webkit-transform: translateX(-100%); /* Firefox bug fix */
 transform: translateX(-100%);
 }
 100% {
 -moz-transform: translateX(100%); /* Firefox bug fix */
 -webkit-transform: translateX(100%); /* Firefox bug fix */
 transform: translateX(100%);
 }
}
</style>
<!-- BODY -->
This is the long-awaited content that I've left as TBD for well over a month. Bask in it's glory.

## Why am I blogging?
For a while now, I've been reading random strings of papers in tutorials loosely tied together by my burgeoning thesis topic. In the process I've learned quite a bit of random information at moderate depth. Usually this level of working understanding gets thrown out, and when it inevitably comes up later for myself or someone else I'm left with a shit ton of buzz words and no substance to feed to my cohort and superiors. Also, I've found that I lack the charisma (integrity?) to bullshit effectively.

I've convinced myself that having a blog to discuss and re-tell what I've learned could help condense what I've learned. Or at any rate it'll help me get a little better at writing in the process.

I'm taking this first blog post, the inaugural blog post, the inblogural post, to take the time to establish what you, the imaginary reader, should expect.

## What to expect when Will's reflecting...
Aside from half-assed jokes, stats, ML, and vague snippets of concepts in genomics, I don't really know how much of a common thread there will be between posts. What I *do* know is that the content is likely to be pretty mixed in format, informal, and I'll probably attempt to be entertaining (for my own sanity). I can say that the following types of content will likely come up:
* Review of specific concepts in stats and ML
* Software tutorials (even with gross trouble-shooting steps)
* Review of *arxiv*, *BioArxiv*, and groups of papers that I feel are related enough to discuss at the same time (mostly it will be me explaining methods)
* Fluffy editorial content about my own research experiences

This article would best be classified as fluff.

Expect everything to be a congfusing mix of formal and informal language (I'll cite legitimate sources when I can so you know when you can tune out). Feel free to comment as long as its relevant to what I post. And most importantly,

<div class="example1">
<h3>Have Fun!</h3>
</div>

Thanks for reading,

William

P.S. Here's the CSS code I wasted 15 minutes of my life scraping together just to make that ironic animation in [Kramdown](https://kramdown.gettalong.org/). [^1]
~~~html
<style>
.example1 {
 height: 50px;
 overflow: hidden;
 position: relative;
}
.example1 h3 {
 font-size: 3em;
 color: limegreen;
 position: absolute;
 width: 100%;
 height: 100%;
 margin: 0;
 line-height: 50px;
 text-align: center;
 /* Starting position */
 -moz-transform:translateX(100%);
 -webkit-transform:translateX(100%);
 transform:translateX(100%);
 /* Apply animation to this element */
 -moz-animation: example1 15s linear infinite;
 -webkit-animation: example1 15s linear infinite;
 animation: example1 15s linear infinite;
}
/* Move it (define the animation) */
@-moz-keyframes example1 {
 0%   { -moz-transform: translateX(-100%);  }
 100% { -moz-transform: translateX(100%); }
}
@-webkit-keyframes example1 {
 0%   { -webkit-transform: translateX(-100%); }
 100% { -webkit-transform: translateX(100%); }
}
@keyframes example1 {
 0%   {
 -moz-transform: translateX(-100%); /* Firefox bug fix */
 -webkit-transform: translateX(-100%); /* Firefox bug fix */
 transform: translateX(-100%);
 }
 100% {
 -moz-transform: translateX(100%); /* Firefox bug fix */
 -webkit-transform: translateX(100%); /* Firefox bug fix */
 transform: translateX(100%);
 }
}
</style>
~~~

[^1]: I had help from *[quackit.com?](https://www.quackit.com/css/codes/marquees/)*
