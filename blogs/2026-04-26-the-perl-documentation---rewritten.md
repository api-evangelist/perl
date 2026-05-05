---
title: "The Perl Documentation - Rewritten"
url: "https://blogs.perl.org/users/petamem/2026/04/the-perl-documentation---rewritten.html"
date: "2026-04-26T18:05:02Z"
author: "PetaMem"
feed_url: "https://blogs.perl.org/atom.xml"
---
<p>Well, not <em>all</em> of it ... yet. But some of it has been rewritten many times in many languages and "all" of it will be rewritten in many more languages. Of course "all" will never be reached, so it will be an ongoing endeavor, but at least you know the goalposts.</p>

<p>You can read it at <a href="https://perl.petamem.com/docs/eng/">https://perl.petamem.com/docs/eng/</a>, and the language picker in the upper right hand corner will tell you, more honestly than any sentence in this post can, where the public-facing part of the work currently stands.</p>

        <h2>What you will find there</h2>

<p>A reworked documentation set for Perl - shipping with pperl, but addressed to the wider Perl audience. It covers the things you would expect (introduction, getting-started, CLI, how-tos, P5 and PP runtime references) and is rendered through a tailored Sphinx pipeline so the navigation, search, and theming behave the way modern documentation sites are expected to behave.</p>

<p>The picker currently shows four languages in colour: English, German, French, Spanish. All four are work in progress. English is the source - the canonical version every other language is translated from - but it is itself being rewritten and reorganised, chapter by chapter, and is not in any sense "done." The other three languages are translations that follow the moving English target. The remaining flags in the picker are greyed: planned coverage, in scripts spanning Latin, Cyrillic, Greek, Hebrew, and Arabic. Languages will move from grey to colour as their translations land. We are not committing to a date on any of them, and we are not committing to the final list either. The picker is a roadmap of work we are confident we can finish, not a wish list.</p>

<p>Readers who followed <em>Rust-PDL Part Two</em> a few days ago will find the corresponding documentation at <a href="https://perl.petamem.com/docs/eng/p5/PDL.html">https://perl.petamem.com/docs/eng/p5/PDL.html</a>. The pattern, in case it is not obvious from the two posts read together: code first, documentation as soon afterwards as we can manage. Documentation that lags the code is documentation nobody trusts.</p>

<h2>Two axes of work</h2>

<p>There are two distinct kinds of work happening here, and they do not always speak to the same reader.</p>

<p><strong>The first is content.</strong> A lot of what ships in the canonical Perl documentation has been with us for a long time, was written under different conventions of technical writing, and shows it. Some of it is excellent. Some of it presumes a reader who has already learned Perl from somewhere else and just needs the reference. The work we are doing on this axis is not a polite refresh of existing prose. It is, in places, a structural rewrite - new organisation, new examples, new emphasis on the things modern Perl users actually run into. The goal is documentation that a Perl programmer in 2026 can read without having to imaginatively reconstruct the assumptions of a Perl programmer in 1998.</p>

<p><strong>The second is translation.</strong> Perl documentation has historically been an English artefact. There are pockets of community translation work, scattered and varying in completeness, but no comprehensive multi-language documentation set in the modern sense. We are building one. The motivation is simple: a developer whose first language is not English currently has, for many languages, exactly zero Perl documentation in their language. The bar to clear, for that developer, is not perfection. It is "better than nothing." That is one piece of a larger picture I do not propose to lay out here. The picker shows the ambition; the four currently active languages (English plus three) show the present.</p>

<h2>A case study: the debugging chapter</h2>

<p>The most concrete way to show what "rewritten" means is to point at one chapter. The debugging guide at <a href="https://perl.petamem.com/docs/eng/guide/debugging/index.html">https://perl.petamem.com/docs/eng/guide/debugging/index.html</a> is structured around what a developer actually does when something is going wrong:</p>

<ul>
<li>Preflight (what to check before reaching for a debugger)</li>
<li>Print and die (the simplest tools, used well)</li>
<li>Inspecting state</li>
<li>The interactive debugger</li>
<li>Breakpoints</li>
<li>Tracing</li>
<li>Exceptions</li>
<li>IDE / DAP integration</li>
</ul>

<p>This is a different shape from the upstream <code>perldebug</code> document, in two ways. The first is structural: each of the eight topics is its own URL, addressable from a search result, rather than a section in one long narrative. The second is depth-layered: each topic exists at three reading depths - an overview that orients, a reference that defines precisely, and a "gory details" layer for the reader who has met a corner case and needs to understand it. This is the shape every guide chapter is moving toward. It serves the reader who arrives with a specific question and the reader who wants to understand the topic seriously, from the same source.</p>

<p>How was this chapter produced? The honest description is: we used an AI as a research assistant, with access to the same kinds of sources a human technical writer would consult - perldoc itself, CPAN module documentation, conference talks, blog posts, mailing-list archives, the source code of the Perl debugger, and one book used with the explicit permission of its author, Richard Foley - and ran several distillation passes over its output. De-obsoleting (removing references to versions and tools nobody runs anymore). De-duplicating (the same advice repeated by different authors collapses into one statement). Synthesising (multiple partial treatments of one topic become a single complete treatment). The methodology is not exotic, but it is genuinely different from "writer sits down and writes a chapter," and it produces results of a kind that "writer sits down" cannot easily reach - because no human writer has read everything that has been written about Perl debugging, and the cost of doing so would be prohibitive.</p>

<p>A note on the obvious question: this is the same activity any technical author performs. Reading existing material on a topic to inform new writing is how technical writing has always worked. Copyright protects expression, not facts; the output is a new piece of writing in a new structure, not a derivative of any one source. The AI changes the scale and speed of what one author can read and synthesise. It does not change the underlying activity. We have been deliberate about this. Human review is not a checkpoint at the end of the process; it accompanies the process, which is iterative and ongoing.</p>

<p>One sequencing detail worth naming. The rewriting described above is the first stage. The translations come after - applied to the rewritten English, not to the upstream original. And translation follows a different discipline from rewriting: faithful, not inventive. We grant ourselves latitude when restructuring an English chapter against thirty-year-old upstream prose. We grant ourselves no such latitude when carrying that chapter into French or German or Spanish - obviously. Compounding deviation across two transformations would defeat the point of doing either one carefully.</p>

<h2>A case study: the build pipeline</h2>

<p>The translation work is one branch of a larger pipeline. Before any translation happens, the English source is assembled out of multiple inputs: hand-authored Markdown, per-function reference files (perlfunc has one Markdown file per built-in, with YAML frontmatter for category tags, signature, and prose body), runtime metadata derived from the pperl source tree, CLI help auto-extracted from the binary's option parsing, and a lint pass that catches the kinds of things linters catch in code: dead links, malformed cross-references, frontmatter schema drift. All of this lands in a staging tree that Sphinx then renders. The source tree is never written to during a build; the staging tree is the contract between the assembly stage and the rendering stage.</p>

<p>Translation hangs off this staging tree. Each target language has its own PO catalogue, identified by ISO 639-3 code (<code>fra</code>, <code>deu</code>, <code>spa</code>, and so on - the three-letter codes are deliberate, because the two-letter ISO 639-1 set runs out of distinctions for several of the languages on our roadmap). The translation passes are run by per-language translator agents that are seeded with terminology consistency rules and a fixed register for technical prose. PO catalogues are merged forward when the English source changes, so a sentence revised on the English side surfaces as a fuzzy entry in every language catalogue and is re-translated rather than silently going stale.</p>

<p>The pipeline handles right-to-left scripts (Arabic, Hebrew) and non-Latin scripts (Cyrillic, Greek) without per-language special casing - the layout is handled at the theme level, which means a new language is, infrastructurally, a new PO catalogue and not a build-system rewrite. That separation is what makes the long roadmap tractable.</p>

<p>Each language renders to two outputs: the HTML site that the picker navigates, and a single large PDF of the whole documentation set. The PDF is not a polite afterthought. There are readers and use cases - offline reading, print, archival, regulated environments - where a self-contained PDF is the format that actually gets used.</p>

<p>Each HTML page also offers a "Source (accessible &amp; AI friendly)" link that returns the page's underlying source rather than its rendered HTML. This is partly conventional - source links are good engineering practice for any documentation site - but it is also a deliberate accommodation for a class of reader we expect to grow: AIs, agents, and other automated consumers of documentation. They do not need the navigation chrome, the syntax-highlighting CSS, or the responsive layout. They need the text, structured. The source links give them that.</p>

<p>Some numbers to give a sense of the translation volume. The <code>perlfunc</code> reference in French alone takes roughly 1.9 million tokens of translation work, split across eight chunks running in parallel, around 22 to 23 minutes per chunk. That is one section, in one language. Multiply by the number of sections, multiply again by the number of languages on the roadmap, and the order of magnitude becomes the point: this is work that historically did not happen in the Perl world because nobody had the resources to do it. We do, now, and we are doing it.</p>

<h2>A note on the difficulty</h2>

<p>It would be easy to read the volume figures and conclude that with a sufficiently large language model and enough patience, multi-language technical documentation is now a solved problem. It is not. The honest description of the work is that it is brutally hard.</p>

<p>Terminology has to stay consistent across thousands of strings within one language and across all languages. The idiomatic register has to match the original's tone, which itself varies by section. Technical precision has to survive translation, which is harder than it sounds when the source language is English and the target language has different defaults for, say, the number of words a sentence can carry before it becomes grammatically ambiguous. Code examples raise their own questions - do you translate variable names? Function names? Error message strings the reader will see in their own terminal? (We do not, mostly, but the question recurs at every chapter.) Right-to-left layouts produce edge cases that no test catches until a human reads the rendered page. AI is the reason this work is feasible at all. But - you know - AI+Perl makes hard things... possible. </p>

<h2>Heads up</h2>

<p>This is a "release early" post. The English documentation is in a state where you can use some of it. The three active translations are in a state where they are useful for the chapters that have landed and unfinished for the chapters that have not. The greyed flags in the picker are work we intend to do; we are not promising any specific date.</p>

<p>If you read Perl in English and prefer documentation that has been organised around modern reading habits, the site is worth a look today. If you read Perl better in another language, the picker shows whether your language is live yet, and the answer for most is "not quite, but coming." If you find errors, things that should be re-organised, or sections that read awkwardly, no surprise there - it is an early shape.</p>

<ul>
<li>Richard C. Jelinek, PetaMem s.r.o.</li>
</ul>
