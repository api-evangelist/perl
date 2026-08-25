---
title: "WebDyne 3.0 released -- now with PAGI, Server-Sent Events and WebSockets"
url: "https://blogs.perl.org/users/aspeer/2026/08/ive-released-webdyne-30-an.html"
date: "2026-08-22"
author: "Andrew Speer"
feed_url: "https://blogs.perl.org/atom.xml"
---
I’ve released WebDyne 3.0, an update to the Perl-based dynamic HTML engine I have created. The biggest addition in 3.0 is support for PAGI, alongside the existing PSGI and Apache/mod_perl backends. PAGI support brings an asynchronous/event-oriented interface to WebDyne and allows WebDyne applications to handle more than conventional HTTP request/response traffic: Server-Sent Events (SSE) for streaming events from Perl applications to browsers WebSocket connections for bidirectional, long-lived connections Normal asynchronous HTTP requests PAGI application lifespan startup/shutdown events WebDy
