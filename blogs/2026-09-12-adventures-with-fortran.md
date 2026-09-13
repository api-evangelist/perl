---
title: "Adventures with Fortran"
url: "https://blogs.perl.org/users/ed_j/2026/09/adventures-with-fortran.html"
date: "2026-09-12"
author: "Mohawk"
feed_url: "https://blogs.perl.org/atom.xml"
---
If you do scientific and/or numerical computing, you probably use or at least know about BLAS , and LAPACK . If you've done much programming with them, you may have passed in data that it cannot handle, and then you'll probably know about xerbla_ . xerbla_ is the error-handler in those two libraries, and by default it terminates the whole process.
