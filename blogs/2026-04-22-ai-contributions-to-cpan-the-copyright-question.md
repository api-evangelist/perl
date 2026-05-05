---
title: "AI Contributions to CPAN: The Copyright Question"
url: "https://blogs.perl.org/users/todd_rinaldo/2026/04/ai-contributions-to-cpan-the-copyright-question.html"
date: "2026-04-22T15:55:52Z"
author: "Todd Rinaldo"
feed_url: "https://blogs.perl.org/atom.xml"
---
<p><em>This is a developer's perspective, not legal advice. I'm not a lawyer. What follows is my personal reading of publicly available licenses, policy documents, and one court decision. If you're making decisions about your module's legal exposure, talk to a lawyer.</em></p>

<p>The open source world is actively debating whether to accept AI-assisted contributions. QEMU, NetBSD, and <a href="https://wiki.gentoo.org/wiki/Project:Council/AI_policy">Gentoo</a> have said no. A lot of CPAN maintainers haven't written down a policy but have a reflex &mdash; if a PR looks AI-assisted, close it without a real review.</p>

<p>Two very different concerns sit underneath that reflex, and they usually get mashed together:</p>

<ul>
<li><strong>Quality.</strong> AI can produce plausible-looking code that doesn't actually work, hallucinates APIs, or subtly misunderstands the problem. This wastes reviewer time.</li>
<li><strong>Copyright.</strong> AI might reproduce memorized training material the contributor has no right to relicense. The output itself may not even be copyrightable. The contributor may not actually own what they're submitting.</li>
</ul>

<p>This article is about the second one. The quality concern is real, but you already know how to handle it &mdash; you read the PR, you run the tests, you ask questions. It's the same concern you have about any contributor. The copyright concern is the structurally novel one, and it's the question where CPAN's particular history matters.</p>

<p>I maintain CPAN modules, and for a while I've been running AI-assisted modernization tools (<a href="https://blogs.perl.org/users/todd_rinaldo/2026/04/575-pull-requests-in-three-weeks-what-happens-when-ai-meets-cpan-maintenance.html"><tt>koan</tt></a> is one example of the category) against the modules I care for. Across the <a href="https://github.com/cpan-authors">cpan-authors GitHub organization</a> &mdash; a collection of repositories where many CPAN modules are collaboratively maintained &mdash; hundreds of those PRs have been merged, every one with a human in the loop: a maintainer reading the diff, running the tests, and taking full responsibility. My argument isn't that nothing has ever been wrong. It's that the copyright concerns people raise about AI-assisted contributions are not a new kind of concern for CPAN. They are the same concern CPAN has always carried, under a different name.</p>

<p>The reflex to reject AI-assisted PRs on copyright grounds quietly smuggles in an assumption: that human-authored CPAN contributions came with a clean bill of provenance, and AI is the thing threatening to pollute the water. That assumption does not survive five minutes of honest thought about how CPAN actually works.</p>

<h2>What CPAN actually verifies</h2>

<p>CPAN's rule for accepting new code is, in full: the author uploads a tarball, declares a license, and we trust them. Many modules pick "same terms as Perl," but plenty use Artistic 2.0, MIT, Apache 2.0, or something else &mdash; and a surprising number ship with an ambiguous or missing license line.</p>

<p>There's no <a href="https://developercertificate.org/">DCO</a>. There's no <a href="https://en.wikipedia.org/wiki/Contributor_License_Agreement">CLA</a>. PAUSE confirms that you are who you say you are. It does not confirm that you own what you just uploaded. When the license is "same terms as Perl" &mdash; still the most common declaration on CPAN &mdash; it points to a moving target: Artistic 1.0 plus GPL 1-or-later. That pair has been tested in U.S. court basically once, in <em>Jacobsen v. Katzer</em> (Fed. Cir. 2008), and never that I know of outside the U.S. The part of Artistic that reliably works is the warranty disclaimer &mdash; and every common CPAN license (Artistic 2.0, MIT, Apache 2.0, GPL) has a disclaimer of its own. Those disclaimers appear, to me, to be doing most of the real legal work for CPAN today.</p>

<p>If you've maintained a module for a while, you already know the quiet risks sitting in the index:</p>

<ul>
<li>Code an employer actually owns, uploaded by an employee who never got permission. Some of this has been in widely-used distributions for decades.</li>
<li>Code copied from a book, a paper, or a reference implementation, with the original copyright never mentioned.</li>
<li>Modules ported from another language without telling &mdash; or asking &mdash; the original author.</li>
<li>Abandoned modules whose authors can't be reached and whose ownership chain is, in practice, lost.</li>
<li>License tags like "same terms as Perl 5.6.1" that point at a license text nobody has read in twenty years, and whose present-day legal force I personally wouldn't want to bet on.</li>
</ul>

<p>None of this has blown up into a real copyright fight. That's not because CPAN is clean. It's because the licenses CPAN actually uses &mdash; Artistic/GPL, Artistic 2.0, MIT, Apache &mdash; are all permissive enough that, as I read them, a plaintiff would have a hard time showing they lost anything. It's because every one of those licenses comes with a warranty disclaimer that blocks most ways of suing in the first place. And it's because the culture of the ecosystem does not go looking for that kind of fight.</p>

<p>This is not a knock on CPAN. It's the cost of a thirty-year-old volunteer archive that chose breadth over lawyering. The trade has held up fine.</p>

<p>But it's the baseline you need to admit before you reject an AI-assisted PR on sight, on copyright grounds alone.</p>

<h2>AI is not a new kind of copyright risk</h2>

<p>Once you look honestly at how CPAN handles contributions, the AI copyright debate stops being about whether to let something dirty into a clean system. It becomes about whether to add one more flavor of provenance uncertainty to a system that has always run on several.</p>

<p>The copyright concerns people raise about AI are real:</p>

<ul>
<li>The model might reproduce copyrighted code it was trained on, without attribution.</li>
<li>Parts of the output may not be copyrightable at all, which weakens the contributor's ability to license it to you.</li>
<li>The contributor may not have a clear legal claim to what they're granting.</li>
</ul>

<p>Now compare those to the copyright concerns that have always been there for CPAN:</p>

<ul>
<li>The contributor's employer might own the code under a work-for-hire arrangement and never agreed to release it.</li>
<li>Part of the module might be a near-copy of a GPL-incompatible reference implementation from a textbook or another project.</li>
<li>Ported-from-another-language code may have the original author's copyright still attached to it in ways the contributor never addressed.</li>
<li>Abandoned modules may have copyright holders who are unreachable and whose heirs could, in theory, assert rights tomorrow.</li>
</ul>

<p>It's the same shape. We're not sure the human who signed for this code had the legal authority to grant the license they claimed, and if they didn't, we have no efficient way to find out. The source of that uncertainty has changed &mdash; it used to be a textbook or an employer, now it might also be a training set &mdash; but the failure mode is the same, and the way CPAN handles it is the same: the human takes responsibility, the warranty disclaimer catches what falls through, and the permissive license protects downstream users.</p>

<p>That's why the pragmatic camp in open source &mdash; Linux kernel, Red Hat, Apache, GitLab, OpenInfra &mdash; has landed where it has: allow AI-assisted contributions with commit-trailer disclosure (GitHub-native projects commonly use <tt>Co-authored-by:</tt>; the kernel uses <tt>Assisted-by:</tt>) and full human responsibility. The strict-ban camp &mdash; QEMU, NetBSD, Gentoo &mdash; quietly assumes the pre-AI baseline was clean. For projects with DCOs and CLAs, that assumption is at least defensible. For CPAN, it isn't.</p>

<h2>What actually changes: volume</h2>

<p>There is one thing AI genuinely changes about the copyright picture, and it's the thing every CPAN maintainer should care about: <strong>volume</strong>.</p>

<p>CPAN's background rate of problematic code &mdash; borrowed from a book, copied out of work-for-hire, lifted from an incompatible-license reference implementation, and now potentially reproduced from a model's training set &mdash; has never been zero, and systematic provenance review has never been the norm on CPAN. What AI changes is that one contributor with a decent model and a decent tool can produce PRs at a rate no individual ever could before. Ship more, roll the dice more.</p>

<p>That's the change worth naming. Not a new kind of risk. Just more throws of the same dice &mdash; which justifies some proportional vigilance, not a categorical rejection.</p>

<h2>How to actually evaluate an AI-assisted PR</h2>

<p>When an AI-assisted PR lands on your module, the quality checks are the ones you already know how to run &mdash; does the change make sense, do the tests pass, does the style match the repo, does the contributor engage when you ask questions. None of that is AI-specific.</p>

<p>The copyright-specific checks are small and cheap:</p>

<ul>
<li><strong>Look for the obvious copy tells.</strong> Anything with copyright headers, SPDX tags, or author-name strings in it should bounce &mdash; those are signs of memorized training material. A quick GitHub search for any distinctive identifier or string literal will catch the worst cases. This scales with the volume.</li>
<li><strong>Expect disclosure.</strong> Ask contributors to mark AI-assisted commits with a <tt>Co-authored-by:</tt> trailer &mdash; the standard GitHub convention, and one Red Hat names alongside <tt>Assisted-by:</tt> and <tt>Generated-by:</tt> as an acceptable option in its <a href="https://www.redhat.com/en/blog/ai-assisted-development-and-open-source-navigating-legal-issues">Nov 2025 analysis</a>. The point is transparency: a reader of the log should be able to see which commits had AI help. Only humans should appear in <tt>Signed-off-by:</tt> lines; an AI has no standing to certify the DCO.</li>
<li><strong>Hold the human accountable, not the tool &mdash; and be clear about which human.</strong> Who is asserting the license grant depends on the workflow. When an external contributor opens a PR, they are the one claiming the right to license their submission; the merge accepts that claim. When you are running an AI tool yourself against modules you maintain, the assertion and the acceptance collapse into a single merge click, and you are the accountable human on both sides. Third-party AI-assisted PRs sit in the normal contributor-plus-maintainer model; self-operated tools compress it. Either way, a human with legal standing is accountable somewhere. If you can't explain what you're merging &mdash; because you didn't review it, or because the contributor can't explain it either &mdash; don't merge it.</li>
</ul>

<p>The difference between a PR you merge and one you reject, on copyright grounds, isn't whether a model was involved. It's whether a human with legal standing to grant the license took responsibility for doing so &mdash; at submission, at merge, or both. That test is the same test CPAN has been running, implicitly, for thirty years.</p>

<h2>One argument to retire</h2>

<p>"CPAN was in the training data, so AI output is CPAN-compatible." Let it go. We don't know what's in Claude's training data, or GPT's, or anyone else's. We do know these models have read Perl from all over GitHub (including incompatible licenses), from Stack Overflow (CC BY-SA), from books, blogs, and anywhere else crawlable. "Trained on CPAN" is a comforting story, but we can't confirm it, and resting an argument on it makes the argument weaker, not stronger.</p>

<p>The honest claim is smaller and more useful. The contributor has reviewed the output. The contributor is accountable. The warranty disclaimer catches the residual risk the same way it has for three decades. That is what the kernel, Red Hat, Apache, and OpenInfra policies all quietly say. It's the claim you can defend &mdash; and it holds whether the tool in the contributor's hand is Claude, GPT, a generous colleague, or a textbook.</p>

<h2>Closing</h2>

<p>The copyright concern with AI-assisted contributions is real, but it isn't new. CPAN has been running on the same legal structure for thirty years &mdash; permissive licenses, warranty disclaimers, contributor accountability &mdash; and that structure handles AI-assisted contributions the same way it handles every other kind of provenance uncertainty CPAN has quietly carried since the beginning. The risk profile is the same. Only the volume is new.</p>

<p>Do the copyright-specific checks when the volume warrants them. Look for the obvious copy tells. Ask for <tt>Co-authored-by:</tt> disclosure. Hold the contributor accountable for the license grant they're making. Trust the warranty disclaimer that's been doing the heavy lifting the whole time.</p>

<p>And update your own internal picture of CPAN while you're at it: it was never a clean room on provenance, and pretending otherwise was always a story we told ourselves.</p>

<hr />
