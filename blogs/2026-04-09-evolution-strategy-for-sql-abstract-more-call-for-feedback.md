---
title: "Evolution strategy for SQL::Abstract::More : call for feedback"
url: "https://blogs.perl.org/users/dami/2026/04/evolution-strategy-for-sqlabstractmore-call-for-feedback.html"
date: "2026-04-09T00:36:45Z"
author: "dami"
feed_url: "https://blogs.perl.org/atom.xml"
---
I am preparing a new version of SQL::Abstract::More , aimed principally at solving several long-standing bugs when param ‘quote_char’ is non-empty (i.e when the user wants to generate SQL of shape like "SELECT `Foo`.`col1`, … FROM `Foo` etc." ). While working on this I need some input from users, because the situation is a bit complicated: Originally SQL::Abstract::More was designed as an extension of the venerable SQL::Abstract and therefore inherited from it, including some internal undocumented behaviors. Then in version 2.0 Matt Trout completely rewrote the internal architecture of…
