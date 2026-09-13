---
title: "Running Perl/PAGI applications on Cloudflare Workers via WebAssembly"
url: "https://blogs.perl.org/users/aspeer/2026/09/running-perlpagi-applications-on-cloudflare-workers-via-webassembly.html"
date: "2026-09-12"
author: "Andrew Speer"
feed_url: "https://blogs.perl.org/atom.xml"
---
Background I've been developing the WebDyne framework to make creation of Perl-based web applications easier (for me anyway). Most of the apps I write now use John Napiorkowski's excellent PAGI design, as it supports modern asynchronous web services such as SSE and WebSockets. One of the challenges has always been: "where do I host them?" They run fine in Docker containers, and the demo website currently runs on Sevalla in a relatively cheap container.
