---
title: "Compiling Google::ProtocolBuffers::Dynamic on Debian Trixie"
url: "https://blogs.perl.org/users/dean/2026/04/compiling-googleprotocolbuffersdynamic-on-debian-trixie.html"
date: "2026-04-16T23:52:36Z"
author: "Dean"
feed_url: "https://blogs.perl.org/atom.xml"
---
I found this sufficient of an obstacle that I wanted to post about it for future posterity. I was able to cpanm Google::ProtocolBuffers::Dynamic after installing these packages on Debian Trixie. build-essential (unsurprisingly) cmake libprotobuf-dev libprotoc-dev The last library eluded me and caused the most frustration. Anyway on to other things.
