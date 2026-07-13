---
title: "JSON::JSONFold - a CPAN module for compact, readable JSON formatting"
url: "https://blogs.perl.org/users/yairlenga/2026/06/jsonjsonfold---a-cpan-module-for-compact-readable-json-formatting.html"
date: "2026-06-30"
author: "Yair Lenga"
feed_url: "https://blogs.perl.org/atom.xml"
---
I've been working on a CPAN module called JSON::JSONFold , and I wrote an article describing the motivation and design. I'd really appreciate feedback from other Perl developers. JSON serializers tend to give us two choices: compact JSON, which is efficient but a dense wall of text that's painful to read, or pretty-printed JSON, which is readable but often wastes a lot of vertical space (a small array of numbers can turn into ten lines).
