---
title: "Peta::NN - Surface Detail"
url: "https://blogs.perl.org/users/petamem/2026/10/petann---surface-detail.html"
date: "2026-10-09"
author: "PetaMem"
feed_url: "https://blogs.perl.org/atom.xml"
---
Peta::NN is a neural network library written in Perl: models are defined, trained, measured and shipped from a Perl script, with no dependency beyond perl 5.36. It is not a binding to somebody else's framework and it does not try to be PyTorch. It trains micro models - a few thousand to a few hundred thousand weights, each answering one narrow question about a string - and composes them: in a pipeline, or fused into one model that runs a whole batch on the graphics card without coming back to Perl in between.
