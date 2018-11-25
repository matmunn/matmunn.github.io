---
title: Open Source
---

It's been an incredibly busy year for me, there's been so much going on that I haven't really gotten
a chance to get to everything that I really wanted to, including my personal side projects.

This has led me to realise that I should open source them in the hopes that someone else might get
some use out of something I've written.

Please see below for links to some of my projects:

<br />
#### Dployr
---
Dployr was a solution for deploying files to a server via FTP after committing them to a git repository.
It watched for changes to the repository via a webhook, got a copy of the changed files and then uploaded
them to a server of your choosing.

There were plans to add all sorts of things - multi-region deployments via AWS and I made a start on integrating
BitBucket and GitHub, among other things.

Unforunately I ran out of time to work on it and it sat on my computer for a while, so now it's open source on GitHub
and avaiable here: https://github.com/matmunn/dployr

<br />
#### Waterfall
---
Waterfall is a scheduling system built on Laravel and Vue. Prior to me building it my workplace used a horrible
Excel spreadsheet to schedule tasks for the coming week. It was incredibly inefficient, prone to not being updated
and if a task got assigned to you during the week you had no way of knowing without being told and then having to
print a new copy of the spreadsheet.

I decided to replace this with a web-based solution, and so far it's been working pretty nicely. It incorporates
Slanger (a Ruby implementation of the Pusher protocol) so that tasks can be seen as they are added on the fly,
it shows native browser notifications and generally keeps everyone more up to date.

I started working on a rebuild of the project after I released it in my workplace but I never got time to finish
it off, life happens. It was more of a cosmetic rebuild than anything, I originally built it with Bootstrap and
didn't pay much attention to styling as I was after quick functionality - I ended up replacing Bootstrap with Bulma
and giving the UI a bit of attention.

Both projects are on GitHub at https://github.com/waterfall


<br /><br/>
If you have any questions about any of my projects, or have suggestions or improvements then don't hesitate to contact
me.
