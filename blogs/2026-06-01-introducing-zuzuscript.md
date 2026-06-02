---
title: "Introducing ZuzuScript"
url: "https://blogs.perl.org/users/toby_inkster/2026/05/introducing-zuzuscript.html"
date: "2026-06-01"
author: "Toby Inkster"
feed_url: "https://blogs.perl.org/atom.xml"
---
So I've created a programming language which blends a fairly JavaScript-like syntax with fairly Perl-like semantics, and a few other features that I haven't really seen in many programming languages. This Perl: use Path::Tiny; my $str = uc(substr(Path::Tiny->new("myfile.txt")->slurp_utf8, 0, 80)); Becomes this in ZuzuScript: from std/path import Path; let str := new Path("myfile.txt") ▷ ^^.slurp_utf8 ▷ ^^[0:80] ▷ uc ^^; The ▷ operator means "evaluate the left side, then evaluate the right side with ^^ set to the result of the left side". It's conceptually similar to | in shells and seems to ma
