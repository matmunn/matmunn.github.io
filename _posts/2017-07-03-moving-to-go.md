---
title: Moving to Go
---

Recently I started experimenting with [Golang](https://golang.org/), the programming language from Google. I'd read about it a bit and heard good things and so I decided that I'd like to give it a go for myself.

To get started I wanted to work on a project that meant something to me, I hate following "Hello, World" examples as they never show the real use cases of a language or framework. I decided that a good place to start would be to experiment with serving an API. In the last month I've used Laravel to write an API for a small side project that incorporates Pusher and some other little bits and pieces.

I essentially wanted to rewrite my Laravel API in Golang just to see how it was done, and so I wanted some nice-to-haves to ease development. I started with using the community-driven [Siris](http://www.go-siris.com/) framework and I've paired it with [Gorm](https://github.com/jinzhu/gorm) to make working with the database very simple.

I started by writing CRUD entries for a group of users and I copied some sample users from the database of the PHP version of the API and tested out the new Golang version.

In the PHP version fetching a list of users from a database running on my local machine takes no less that 140ms, I couldn't get it any faster than that. To fetch the same data in Golang from the same database it takes a mere 2ms - 71x faster than the equivalent script on a Laravel 5.4 installation.

This made me push on with converting my API,  I've since converted the entire thing, with similar performance gains throughout. I'm now intending to push this API into production and see how it fares. It's been a pretty good experiment so far and I'm looking forward to getting a bit handier at Go.

One thing I have noticed compared to PHP is that it doesn't seem to be as concise - some things seem to be a bit wordier than what I'm used to writing. I also love writing applications in Laravel, it's got so many nice things that would be hard to leave behind and it has a super helpful community.

For now I'll continue my experiment with Golang and see where it leads me, it's been worth it so far. I would definitely recommend having a play and seeing if it solves a problem that you may have.
