---
title: "Faster UTF-8 Validation"
url: "https://blogs.perl.org/users/chansen/2026/04/faster-utf-8-validation.html"
date: "2026-04-16T22:16:13Z"
author: "Christian Hansen"
feed_url: "https://blogs.perl.org/atom.xml"
---
A while back, I received a pull request suggesting that I update the performance comparison with Encode.pm in my module, Unicode::UTF8 . When I originally wrote Unicode::UTF8 , Encode.pm used its own UTF-8 validation implementation. Since then, Karl Williamson has done extensive work improving Perl, and Encode.pm now relies on those validation routines based on Björn Höhrmann’s UTF-8 DFA decoder .
