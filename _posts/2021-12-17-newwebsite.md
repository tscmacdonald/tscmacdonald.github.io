---
layout: post
title: Building a personal website
description: If you can read this it's probably working
date: 2021-12-17
tags: computers, web
categories: personal
---


I've been thinking for a while that it would be good to start a personal website, both as a collection of thoughts in one place and as a personal portfolio. Finding the right solution took a little while and a few false starts. My first thought was Wordpress, either as a managed or self-hosted solution. I'd tried a few small managed blogs through wordpress.com before but had found it both limited and complicated to customise. Squarespace, another managed website solution, was unsatisying for similar reasons. Self-hosted Wordpress seemed like it could be a better option, but getting a site up and running had always proved more challenging than I'd expected and as a self-taught amateur server admin I was cautious about the security implications of running a publicly-exposed WP site from my home LAN.

Finally, I found some discussion on Twitter about using GitHub Pages for an easily-configurable personal website and was convinced almost immediately. Here are a few advantages of Pages, as I see them:

* Free hosting with minimal restrictions for a small (<1 GB) site
* Static site design built with [jekyll](http://jekyllrb.com/): web pages are lightweight HTML, served quickly and efficiently.
* All content (text and media) stored and edited as plain files in a legible directory structure making it easy to find, add, and edit content. Text content written as standard markdown.
* Everything stored in a standard repository, making it fast and easy to transfer to a self-hosted site if needed.

All in all, it's a great solution if you're someone that's computer-literate enough to write markdown and occasionally tinker with HTML, but not enough of a web developer to write your own CSS or [keep your Apache updated](https://en.wikipedia.org/wiki/Log4Shell). To make things even easier, there are plenty of themes available on GitHub to fork and use as a starting point. I only considered a handful but ended up settling on [al-folio](https://github.com/alshedivat/al-folio) as a minimal theme with built-in support for blogging, projects, and an academic bibliography.

So far, I'm happy with this setup. Building from plaintext files gives me the freedom to write and edit the way I want to, and it's nice to have a little more exposure to jekyll and git. If you like the look of this site, you're more than welcome to fork the [underlying repository](https://github.com/tscmacdonald/tscmacdonald.github.io/) and use it as a base for your own work - feel free to get in touch if you need a hand getting things working from that point, and I'll see what I can do to help.