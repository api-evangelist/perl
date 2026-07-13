---
title: "Introducing constant::string and constant::string::uc"
url: "https://blogs.perl.org/users/james/2026/06/introducing-constantstring-and-constantstringuc.html"
date: "2026-06-29"
author: "James"
feed_url: "https://blogs.perl.org/atom.xml"
---
If you're like me, you use a constant a lot (I may overuse it). I often use it to turn typos in words and fields into compile-time errors, and for that I usually create constants that either are the named the same as the word, or the word uppercased, like this use constant +{ SERVICE => 'Service', INSTANCE => 'Instance' }; or use constant +{ map +( $_ => $_ ), @constants } and doing that too many times inspired the creation of constant::string and constant::string::uc . Basically they are very thin wrappers over constant, creating the words as constants, either as is or in uppercase The equiva
