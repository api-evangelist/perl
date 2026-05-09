---
title: "Ideas for the CPAN Meta v3 Specification"
url: "https://blogs.perl.org/users/robert_rothenberg/2026/05/ideas-for-the-cpan-meta-v3-specification.html"
date: "2026-05-04"
author: "Robert Rothenberg"
feed_url: "https://blogs.perl.org/atom.xml"
---
At the 2026 Perl Toolchain Summit Salve Nilsen and I proposed some ideas that we have been discussing on and off for the past several months for CPANSec, for a CPAN Meta v3 Specification. Why does the specification need to be extended? Version 2 of the CPAN Meta Spec (CPAN distributio n metadata specification) is does not allow the addition of new data, except using fields prefixed by "x_". However, there is a need to include additional metadata about: external dependencies (services, libraries, files, or environment variable) embedded external libraries, e.g. zlib or bootstrap.
