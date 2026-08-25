---
title: "PAGI 0.002002: Clarifying How Applications Are Loaded"
url: "https://blogs.perl.org/users/john_napiorkowski/2026/08/pagi-0002002-clarifying-how-applications-are-loaded.html"
date: "2026-08-21"
author: "john napiorkowski"
feed_url: "https://blogs.perl.org/atom.xml"
---
Introduction (crossposted from dev.to ) PAGI 0.002002 is a specification release. It does not change the runtime shape of a PAGI application. A running application is still one asynchronous code reference: async sub app { my ($scope, $receive, $send) = @_; await $send->({ type => 'http.response.start', status => 200, headers => [[ 'content-type', 'text/plain; charset=utf-8' ]], }); await $send->({ type => 'http.response.body', body => 'Hello from PAGI!', more => 0, }); } What the release clarifies is how a general-purpose runner may reach that runtime boundary.
