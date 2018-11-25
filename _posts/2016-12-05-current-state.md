---
title: Current State
---

I am definitely not as active as I should be in posting updates to my site, I've been super busy lately and things like this slip my mind, it feels like I have so many things that I need to focus on at once and, sadly, my own projects need to go by the wayside sometimes.

On the Friday just gone I received my new MacBook Pro. I ordered the 15" model with a touchbar and it is the first Mac I've owned in 7 years. Working in a creative environment it is no longer feasible to work on a linux system, everyone around me is creating assets that I am required to access in programs like Adobe InDesign and Photoshop and there is just no Linux version available. Sure, there are programs like GIMP but I've just found it so awful to use, it just doesn't really stack up.

I'm fairly happy with the MacBook though, it's been fairly responsive and it's still a Linux-style environment so I'll definitely be able to make do.

I decided to have a crack at a project to try it out and so I redesigned my website over the weekend. I've moved away from using October CMS to using a new tool I heard about - [Hugo](http://www.gohugo.io). My site is now a static site built with Hugo and instead of using a VPS, my site is now hosted on Amazon S3.

I've been playing with AWS while I built out [dployr](http://dployr.io) and I've been fairly happy with the whole system. One realisation that I've had (and entirely too late) is that I don't always need dynamic content. On my site there is nothing at all that is dynamic and so I didn't need  a VPS just to run my server. It's a complicated set up and one that in wholly unnecessary, the simpler my life is then the better that is for me.

The reason I chose Hugo for my site is its simplicity and its flexibility, as well as the very fast site build time.

![](/img/screenshots/hugo-build-time.png)

Granted that my site is very small, but only 9ms to build the 12 pages is pretty nice. I'd like to make a push at my work to start using something like this in our sites, as our sites are also mostly static.

That's my update for now anyway, I'll try and become more active in the near future.
