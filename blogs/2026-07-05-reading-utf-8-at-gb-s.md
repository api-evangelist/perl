---
title: "Reading UTF-8 at GB/s"
url: "https://blogs.perl.org/users/chansen/2026/07/reading-utf-8-at-gbs.html"
date: "2026-07-05"
author: "Christian Hansen"
feed_url: "https://blogs.perl.org/atom.xml"
---
A couple of months ago I wrote about a UTF-8 library I implemented in C, which Unicode::UTF8 uses under the hood: Faster UTF-8 validation . I then updated PerlIO::utf8_strict to use the same library. PerlIO::utf8_strict is a joint project with Leon Timmermans, who is the PerlIO wizard, while I know a bit about UTF-8.
