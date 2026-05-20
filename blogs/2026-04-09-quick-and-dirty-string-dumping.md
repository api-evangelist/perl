---
title: "Quick and dirty string dumping"
url: "https://blogs.perl.org/users/mauke/2026/04/quick-and-dirty-string-dumping.html"
date: "2026-04-09T13:15:33Z"
author: "mauke"
feed_url: "https://blogs.perl.org/atom.xml"
---
Sometimes, when you're trying to debug encoding issues in Perl code, it is useful to quickly get an idea of what code points Perl thinks are in your string. The straightforward approach of say $string (or print $string ) isn't a good way to look at an unknown string: The results depend on what encoding layers (if any) are set on STDOUT and how your terminal renders the resulting bytes. In some cases, "\xe2\x82\xac" (a three-character string, UTF-8 bytes) may look identical to "\x{20ac}" (a one-character string, Unicode text) when printed, for example. (And some control characters are…
