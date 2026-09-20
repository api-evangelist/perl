---
title: "Two Optimisation Tasks in the Weekly Challenge 391"
url: "https://blogs.perl.org/users/e_choroba/2026/09/two-optimisation-tasks-in-the-weekly-challenge-391.html"
date: "2026-09-14"
author: "E. Choroba"
feed_url: "https://blogs.perl.org/atom.xml"
---
Array Median We are given two sorted arrays, our task is to merge them and return the median. Let’s start with the naive approach: just let Perl sort the list and select the median. #!/usr/bin/perl use warnings; use strict; use experimental qw( signatures ); sub array_median_naive($arr1, $arr2) { my @m = sort { $a $b } @$arr1, @$arr2; return unless @m; return @m % 2 ?
