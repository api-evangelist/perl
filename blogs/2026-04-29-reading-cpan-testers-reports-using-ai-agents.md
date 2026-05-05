---
title: "Reading CPAN Testers Reports Using AI Agents"
url: "https://blogs.perl.org/users/preaction/2026/04/reading-cpan-testers-reports-using-ai-agents.html"
date: "2026-04-29T12:35:39Z"
author: "preaction"
feed_url: "https://blogs.perl.org/atom.xml"
---
<p><a href="https://cpantesters.org">CPAN Testers</a> produce a lot of data. Every <a href="https://cpan.org">CPAN</a> distribution gets tested by our volunteers almost immediately after upload. These testers run every version of Perl across every platform you can imagine, and some you never knew existed. Instead of each project maintaining its own testing environments, the community maintains these systems so the project developers can focus on developing their project. There are more than 150 million test reports so far, and that number currently grows by about one million every month.</p>

<p>Sorting through all of those test reports is a big job. The community helps: Slaven Rezić, Andreas König, and others regularly submit tickets to a project's bug tracker for problems revealed by the testing systems they maintain. And individual maintainers can visit one of the UIs to view the data like <a href="https://fast2-matrix.cpantesters.org">the CPAN Testers Matrix</a> (by Slaven) or <a href="https://magpie.cpantesters.org">CPAN Testers Magpie</a> (by Scott Baker). But this, too, is a lot of manual effort.</p>

<p>Large Language Models (LLM) or "AI" agents have recently arisen as a way to chew through large data sets to produce summaries, even if the data is not well-formatted or "machine-readable." By making requests in plain language, a human can tell an agent to fetch data, analyze it, reformat it, compare it, and produce reports. This year, at <a href="https://perltoolchainsummit.org/pts2026/">the 2026 Perl Toolchain Summit in Vienna Austria</a>, I have built <a href="https://mcp.cpantesters.org">an interface so agents can easily discover and analyze the CPAN Testers data using the Model Context Protocol (MCP.)</a></p>

        <p>By pointing your agent at <a href="https://mcp.cpantesters.org">https://mcp.cpantesters.org</a>, you can ask for CPAN Testers reports for any distribution, and your agent can give you a composite of which tests are failing on which Perl versions and platforms and even suggest fixes! CPAN authors can even ask for a summary across all of their projects to find easy things to fix when they've got a few minutes free. If your agent has scheduled tasks, you can get daily digests of all the test failures from the last day, a feature that was once part of the CPAN Testers website, now entirely customizable to your preferences. If you'd like to help expand the possibilities for agent integration, join <a href="https://github.com/cpan-testers/mcp">the CPAN Testers MCP project on Github</a>.</p>

<p>I'm not that experienced yet with using these agents, but here are some quick examples I made while testing the MCP integration with the Claude desktop application:</p>

<blockquote>
  <p><a href="https://claude.ai/share/941df0f8-421f-47fc-8ab1-cd01a68e95d6">"list test reports for all of PREACTION's dists and check for fails"</a></p>

<p><a href="https://claude.ai/share/96c89a4f-a9a6-49cc-a141-41135428ea00">"List all failing test reports from the last month for distributions by SRI analyze text for issues that are easy to fix."</a></p>
</blockquote>

<p>That second query impressed me. With this, CPAN authors could remove a lot of the tedium from diagnosing failures from user test reports!</p>

<p>This work was made possible by <a href="https://perltoolchainsummit.org/pts2026/sponsors.html">the sponsors of the 2026 Perl Toolchain Summit in Vienna, Austria</a>: <a href="https://www.perlfoundation.org/">The Perl and Raku Foundation</a>, 
<a href="https://www.grantstreet.com/">Grant Street Group</a>,
<a href="https://geizhals.de/">Geizhals Preisvergleich</a>,
<a href="https://vienna.pm.org/">Vienna.pm</a>,
<a href="http://www.suse.com/">SUSE</a>,
Trans-Formed Media LLC,
<a href="https://www.ctrlo.com/">Ctrl O</a>,
<a href="https://www.simplelists.com/">Simplelists</a>,
Harald Joerg,
Michele Beltrame (<a href="https://www.blendgroup.it/">Sigmafin</a>,
Laurent Boivin.</p>
