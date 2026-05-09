---
title: "Signing CPAN Releases with SigStore"
url: "https://blogs.perl.org/users/timothy_legge/2026/05/signing-cpan-releases-with-sigstore.html"
date: "2026-05-07"
author: "Timothy Legge"
feed_url: "https://blogs.perl.org/atom.xml"
---
Signing CPAN Releases with SigStore At the most recent Perl Tool Chain Summit (PTS) in Vienna we decided to deprecate Module::Signature. Module::Signature has been around for a long time but it has become increasingly clear that it does not provide the security assurances that it was designed to deliver. Dist::Zilla::Plugin::SigStore::SignRelease is a new plugin that signs your CPAN release with SigStore before uploading. SigStore uses short-lived, OIDC-issued certificates. You authenticate with Google, GitHub, or Microsoft, and cosign produces a signature bundle.
