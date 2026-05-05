---
title: "AI as a Chance - Opinion"
url: "https://blogs.perl.org/users/petamem/2026/04/ai-as-a-chance.html"
date: "2026-04-23T16:17:26Z"
author: "PetaMem"
feed_url: "https://blogs.perl.org/atom.xml"
---
<p>Use AI. Use it more and better. If you are not yet equipped to use it
well - that is fine, learning takes time - but please do not inhibit
those in the community who are.</p>

<p>That is the whole argument. The rest of this piece is why I think it
is correct, and why I think the current register of the Perl community
around this topic is costing us something specific and avoidable.</p>

        <h2>Who is saying this, and why that matters</h2>

<p>PetaMem, an AI company, was founded in 2001. I ran it - still do.
My MSc is from an AI department. I was doing neural networks in
the 1990s, when the field was still in one of its winters and the word
"AI" was something one did not put on a grant application. I have not
stopped working on this for thirty years.</p>

<p>Which makes me exactly the kind of person whose opinion on AI should be suspected of motivated reasoning. Someone who has built a career on a technology has an obvious incentive to tell you it is good. You are safe, because I have spent most of my adult life living with a particular internal watchdog that distrusts convenient conclusions - the INTJ tendency to run every thought through a "is this actually right?" pass before letting it speak (even then it does not stop). For the record: I don't share the fear of AI that many seem to feel - won't pretend I do.</p>

<p>In 2012 I gave a keynote at the London Perl Workshop about "Perl Strategy". You know: how to make Perl great again. It resulted in the
formation of Propaganda.pm, an effort aimed at improving Perl's public
standing and institutional visibility. I ceased effort with
Propaganda.pm around 2017, for lack of enthusiasm from the
community. No worries: I am not restarting it - this piece is not a
campaign. It is one text, offered once, because something specific has
changed since 2017 - the arrival of a technology that alters the
arithmetic of what a small group of people can do - and the
implications matter for Perl in particular.</p>

<h2>What has changed</h2>

<p>The rate of capability improvement in general-purpose AI over the last
eighteen months is not the rate most people have updated their priors
at. Scepticism acquired six months ago is already out of date. What is
worse, that calcification biases your judgment in the present: the
model that frustrated you then has been replaced - possibly more than
once - by something that behaves differently, fails differently,
succeeds differently, and wants different things from its user. You
are evaluating today's capability through a lens shaped by a version
that no longer exists. Updating in the face of rapid change is the
only honest response to it.</p>

<p>"AI slop" is real. Bad AI-generated code exists and is ubiquitous. But
if you look carefully at where the slop comes from, the pattern is
almost always the same: the failure is not in the model. The failure
is in the interface between the model and the task - what was asked,
how it was asked, how the context was prepared, how the output was
reviewed, what was done with it afterward. A skilled operator and an
unskilled operator, using the same model on the same task, produce
radically different output. We have all the evidence we need that this
is true; we just do not often name it, because naming it is
uncomfortable. "Slop" is, in the great majority of cases, a
description of a process rather than the product of this technology.</p>

<h2>The scale nobody is quite talking about</h2>

<p>Here is an observation I find more interesting than any
benchmark. When I ask an AI to estimate how long a task will take, the
estimates it produces are clearly calibrated on training data from
human developer estimates - "three weeks", "a month", that sort of
thing. I have found, repeatedly and consistently, that those estimates
are off by a factor that lives somewhere in the ballpark of a
thousand. Give or take. The AI is, in a literal sense, unable to see
its own impact. It is estimating how long it would take a human
without AI to do the work, because that is what its training data
contains.</p>

<p>I am not sure people have fully internalised what this means. The
models cannot currently estimate the productivity of humans using
them, because the training data for that does not yet exist at
scale. Which means that even the people who use AI every day are
operating with intuitions that were formed before the current
capability existed, and which the AI itself cannot correct. The
feeling of "this took me three days" and the reality of "this
represents three months of pre-AI work" can coexist in the same person
without the person noticing the gap.</p>

<p>What this adds up to, for someone who has learned to use the tool well
and who picks the right problems to aim it at: the output of a single
individual can easily exceed what was previously the output of a
medium-sized development team. My current conservative estimate of my
own output relative to a standard human-only development team is fifty
to one hundred. This is not a claim about me specifically. It is a
claim about what the ceiling is, for any individual developer who
applies themselves to learning the craft of AI-assisted work. The
ceiling was not this high eighteen months ago. It is this high now.</p>

<p>You do not have to take my word for this. The 575-commits-in-a-week
event that has been discussed recently in the Perl community is an
instance of the same phenomenon. The community has seen the
output. The response has mostly been to focus on fifteen or twenty
commits out of the 575 that were weak. I want to come back to that
response below.</p>

<h2>A different job, not a faster one</h2>

<p>It is tempting to describe what changes with AI as "becoming a faster
developer". That is the wrong frame. The metaphor I keep coming back
to is a naval one.</p>

<p>In the old ecosystem, programmers were sailors. You made sure the
bulkheads were closed, the galley was filled, the deck was
swabbed. You were good or bad at your job depending on how well you
pulled the ropes. With AI used well, you stop pulling ropes. The ropes
get pulled. You become, if you choose to, an admiral - someone who
orders a fleet to take a strategic position around a group of isles,
who makes directional choices, who reviews outcomes, who
integrates. You are not doing the old job faster. You are doing a
different job.</p>

<p>This has implications that are worth sitting with. Experience and
judgment matter more in the admiral's job than in the sailor's job,
not less. The admiral's chief skill is knowing what ought to be done,
what a good result looks like, and when the fleet's output is
off-course. That is exactly the skill a senior developer has
accumulated. The replacement narrative - "AI will take our jobs" -
gets the transition backwards. The people whose jobs are most at risk
are the ones whose work consists of pulling ropes that AI can now
pull. The people whose value goes up are the ones with enough
experience to direct the fleet. If you have been in this profession
for ten or twenty years, the capability that has just arrived is not
your threat. It is your lever.</p>

<h2>The fear, named accurately</h2>

<p>I want to talk about what is happening in the community around AI,
because I think we are having the wrong debate.</p>

<p>Quality concerns about AI-generated code are legitimate. There is bad
AI-generated code. There are real code-review cases where AI-produced
output made a codebase worse. People evaluating individual
contributions on their merits and finding them wanting are doing the
work that code review is supposed to do. None of what follows
contradicts any of that.</p>

<p>But the debate in the community is not, structurally, a debate about
quality. It has a specific shape. Out of 575 commits, fifteen or
twenty bad ones get selected and made representative of the
whole. That selection is not a quality evaluation. No dispassionate
evaluator, trying to characterise a body of work, would pick from the
worst 3% and treat it as the norm. The consistency of this pattern -
across many individuals, many contexts, always selecting in the same
direction - tells us that something other than quality evaluation is
happening.</p>

<p>Consider how we handle this in the case of human developers. We have
all encountered good developers and bad developers. Some
human-produced code is excellent; some is a disgrace. We do not, on
the basis of the disgraceful code, conclude that human developers as a
class should be treated with suspicion. We evaluate individuals on
their individual output. We extend to other humans, by default, the
courtesy of being judged on their specific work in its specific
context.</p>

<p>The same courtesy is not being extended to AI-assisted contributions
in the current community register. A class-wide judgment is being
drawn from a selected subset of output, in a way we would recognise as
unfair if applied to any other category of contributor. The
inconsistency is not subtle. And the consistency of the
inconsistency - across many people, many threads, many contexts,
always in the same direction - suggests that what is being expressed
is not an evaluation. It is something else.</p>

<p>The honest name for that something else, in most cases, is fear of
obsolescence. It is not shameful. It is one of the most predictable
human responses to rapid capability change. But fear dressed as a
quality argument is not an argument, and treating it as one means we
are debating a simulation of the real disagreement.</p>

<h2>The cost</h2>

<p>A community that spends its AI debate in this form is a community not
spending that time learning the tool. The members who are already
skilled at using it do not pay the cost - they adapted, they moved on,
they are building things. The cost is paid by the members who are not
yet skilled and who are not receiving social permission from their
peers to become skilled in public. In a community where the dominant
register around AI is suspicion, experimenting with AI publicly is
socially expensive. That expense is a tax on exactly the learning the
community most needs to be doing.</p>

<p>A management mentor of mine once told me: "I have never seen a company
go bust because it had to. All the companies I have seen go bust did
so because they committed suicide." At the time I thought he was
wrong - surely external circumstances, markets, competition. He was
not wrong. Every declining community I have watched up close has
declined by choice, one quiet decision at a time, each decision
looking reasonable in isolation, the collective arithmetic only
visible in retrospect. The companies my mentor described did not vote
to commit suicide. They just kept making small reasonable-seeming
choices that added up to it.</p>

<p>The Perl ecosystem has been on a cooling trajectory for a long
time. The exponential drop is far behind us; we are in the long tail
now, and the long tail may persist for a long time. Like a white
dwarf, still radiating, nowhere near its former brightness. This is
not a eulogy. White dwarfs are stars. They persist. What they do not
do is get brighter on their own, without something changing the
equations they are operating under.</p>

<p>AI is a change in the equations. It is the largest change in the
equations of software development in the lifetime of anyone reading
this. It is also a change that rewards exactly the kind of judgment
that an experienced community has accumulated. The ecosystem problem
of Perl - and I say this with affection, having worked on it for
decades - is fundamentally a problem of hands. There are not enough of
us to maintain what exists, let alone to expand it.</p>

<p>A community that arrives at this change and chooses to spend its
collective time on the 3% that is bad, rather than on the 97% that
demonstrates what is now possible, is a community making the small
reasonable-seeming choice that my mentor described. And if the pattern
continues, the arithmetic will do what it does.</p>

<p>The tools are here. The question is whether we embrace them.</p>

<p>My answer is hereby on record.</p>

<ul>
<li>Richard C. Jelinek, PetaMem s.r.o.</li>
</ul>
