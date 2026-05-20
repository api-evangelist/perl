---
title: "Installing Bit::Vector on Debian 13 (Trixie)"
url: "https://blogs.perl.org/users/dean/2026/05/installing-bitvector-on-debian-13-trixie.html"
date: "2026-05-16T13:53:21Z"
author: "Dean"
feed_url: "https://blogs.perl.org/atom.xml"
---
Whilst Bit::Vector is available as a Debian package in libbit-vector-perl , when installing it using cpanm the compile failed for me. The installation crashed during the make stage, throwing a specific compiler error regarding false and true tokens: Failure Output: Building Bit-Vector-7.4 ... cc -c -D_REENTRANT -D_GNU_SOURCE -fwrapv -fno-strict-aliasing -pipe -fstack-protector-strong -I/usr/local/include -D_LARGEFILE_SOURCE -D_FILE_OFFSET_BITS=64 -D_FORTIFY_SOURCE=2 -O2 -DVERSION=\"7.4\" -DXS_VERSION=\"7.4\" -fPIC…
