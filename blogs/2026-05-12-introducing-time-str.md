---
title: "Introducing Time::Str"
url: "https://blogs.perl.org/users/chansen/2026/05/introducing-timestr.html"
date: "2026-05-12T22:28:22Z"
author: "Christian Hansen"
feed_url: "https://blogs.perl.org/atom.xml"
---
Time::Str is a Perl module for parsing and formatting date/time strings across 20+ standard formats. It has an optional C/XS backend, nanosecond precision, and rejects input it cannot parse unambiguously rather than guessing. use Time::Str qw(str2time str2date time2str); my $time = str2time('2024-12-24T15:30:45Z'); # 1735052445 my $str = time2str($time, format => 'RFC2822', offset => 60); # 'Tue, 24 Dec 2024 16:30:45 +0100' Standards Compliance Each format is implemented according to its specification: RFC 3339, RFC 2822, RFC 2616, ISO 8601 (calendar dates), ISO 9075, ITU-T X.680 (ASN.1),…
