---
title: "perl-lsp version 0.6.0"
url: "https://blogs.perl.org/users/veesh/2026/07/perl-lsp-version-060.html"
date: "2026-07-05"
author: "Veesh"
feed_url: "https://blogs.perl.org/atom.xml"
---
I'm pleased to announce the release of perl-lsp version 0.6.0; you can install it from Github releases, from crates.io via cargo install perl-lsp , or as a vscode or vscodium extension. If you are a zed user, you can opt in using the zed-perl extension following these instructions . Notable new features in this version: - Type Narrowing - ref/isa/defined checks and early returns will type the checked variable for the duration of the block as relevant - Diagnostics - warnings if your code is dereferencing against a known or possibly undef value, or otherwise incompatibly (methods from the wrong
