---
title: "CPAN Dependencies, static and dynamic"
url: "https://blogs.perl.org/users/grinnz/2026/04/cpan-dependencies-static-and-dynamic.html"
date: "2026-04-12T02:45:28Z"
author: "Grinnz"
feed_url: "https://blogs.perl.org/atom.xml"
---
Dependencies or prerequisites are an integral feature of the CPAN software repository. They define what other CPAN modules are required for a particular CPAN distribution to be built, tested, or ultimately to function, as well as optionally to improve or add functionality. To define them properly for a distribution, it is helpful to understand exactly how they will be used, and what all the different distribution files like Makefile.PL , Build.PL , META.json , and MYMETA.json are for. sidebar: In this post, I will focus on the "requires" relationship for dependencies, which are hard…
