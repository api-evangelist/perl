---
title: "Importance of Repositories in Public"
url: "https://blogs.perl.org/users/mikko_koivunalho/2026/04/importance-of-repositories-in-public.html"
date: "2026-04-24T00:39:44Z"
author: "Mikko Koivunalho"
feed_url: "https://blogs.perl.org/atom.xml"
---
<p>It used to be so that a <strong>repository</strong> was only a place of work
and the <strong>distribution</strong> was the actual result of that work.
Only the contents of the distribution mattered. People would
read the files <code>README</code> and <code>INSTALL</code> from the distribution
after having downloaded it.</p>

<p>Not so anymore. Today the repository is out in the open in
<a href="https://www.github.com">GitHub</a>,
<a href="https://www.gitlab.com">GitLab</a>,
<a href="https://codeberg.org/">Codeberg</a>
or other shared hosting site.
On the other hand, the documentation in the distribution is often
discarded as distribution packages are rarely downloaded manually
but rather via a package manager which installs them automatically.</p>

<p>Publicly viewable repository has in fact become much more
than just a place of work. It is also an advertisement
for the project and of the community behind it, if there is
more than one author or contributor.</p>

<p>When a potential user first finds the project repository,
the hosting site commonly presents him with the project <code>README</code>
file. That makes <code>README</code> file in fact the <strong>welcome page</strong>
to the project. Its purpose is changed from being purely
informational to being an advertisement which
competes for user&#8217;s attention with bright colors,
animated pictures, videos and exciting diagrams, shapes
and &#8220;bumper stickers&#8221;.</p>

<p>But under all the exciting cover it must also remain
true to its nature: present the project
as precisely as possible and stay up to date with
its development.</p>

<p><code>README</code> might also not be the only file which needs
to be kept up to date because it is accessed in the (public) repository.
Other potential files can include
<code>INSTALL</code>, <code>Changes</code> and <code>CODEOWNERS</code>.</p>

<p>Many files therefore contain text which
must be updated at least at the time of release:
version numbers, API documentation, examples,
file lists.</p>

<p>It is difficult to keep these files in sync
with the code; just like documentation, which fact
every programmer knows. The <a href="https://metacpan.org/dist/Dist-Zilla">Dist::Zilla</a>
plugin <a href="https://metacpan.org/dist/Dist-Zilla-Plugin-WeaveFile">Dist-Zilla-Plugin-WeaveFile</a>
will prevent the files from falling out of sync
because their content is tested continuously.</p>

<p>There are other ways to do this, for instance
<a href="https://metacpan.org/dist/Dist-Zilla-Plugin-CopyFilesFromBuild">Dist::Zilla::Plugin::CopyFilesFromBuild</a>.</p>

<p>It is my philosophy that nothing in the repository
is changed <em>behind programmer&#8217;s back</em>.
It can also be dangerous to the programmer
if he is not a frequent Git committer.
Failed local tests are much safer.
And when the test fails, it is easy
to run <code>dzil weave</code> to update the files.</p>

<h1>Dist-Zilla-Plugin-WeaveFile</h1>

<p>The plugin <a href="https://metacpan.org/dist/Dist-Zilla-Plugin-WeaveFile">Dist-Zilla-Plugin-WeaveFile</a> works very much like my earlier plugin <a href="https://metacpan.org/dist/Dist-Zilla-Plugin-Software-Policies">Dist-Zilla-Plugin-Software-Policies</a>: it consists of three pieces: The Dist::Zilla command <code>weave</code>, the plugin <code>WeaveFile</code> which is used to define the configuration in <code>dist.ini</code> file, and the plugin <code>Test::WeaveFile</code> which creates tests for the distribution which check that the defined files exist and match their definition.</p>

<p>Example from <code>dist.ini</code> file:</p>

<pre><code>; Uses default config file .weavefilerc
[WeaveFile / README.md]

; Uses a custom config file and specifies file explicitly
[WeaveFile]
config = install-weave.yaml
file = INSTALL

[Test::WeaveFile]
</code></pre>

<p>And the definition file <code>.weavefilerc</code> would then contain, for example:</p>

<pre><code>---
snippets:
    badges: |
        [![CPAN](https://img.shields.io/cpan/v/My-Dist)](https://metacpan.org/dist/My-Dist)
    license: |
        # LICENSE
        [% USE date -%]

        This software is copyright (c) [% date.format(date.now, '%Y') %] by [% dist.author %].

        This is free software; you can redistribute it and/or modify it under
        the same terms as the Perl 5 programming language system itself.
files:
    "README.md": |
        [% snippets.badges %]

        # [% dist.name %] - [% dist.version %]

        [% dist.abstract %]

        [% pod("My::Module", "SYNOPSIS") %]
        [% pod("My::Module", "DESCRIPTION") %]

        [% pod("bin/myprog", "EXAMPLE") %]

        [% snippets.license %]
</code></pre>

<p>The templating system is <a href="https://metacpan.org/dist/Template-Toolkit">Template-Toolkit</a>.
I am planning to change this so that user can choose another templating system if wanted, and then Template-Toolkit will be optional to install. Also allowing to change the output format (currently Markdown) is in plans. All pod text is converted to Markdown.</p>

<p>With a configuration like the above, when user runs <code>dzil test</code>, if the static files <code>README.md</code> and <code>INSTALL</code> are not in sync with their definitions, user can run:</p>

<pre><code>dzil weave
</code></pre>

<p>or</p>

<pre><code>dzil weave README.md
dzil weave INSTALL
</code></pre>

<h1>Future</h1>

<p>There might be additional generated information which we will be forced - for practical reasons - to commit into the repository. <code>cpanfile</code> could be one such. GitHub repositories are being scanned by different AI tools which could draw benefit from having such information at hand, instead of being generated and only available in the distribution in <a href="https://metacpan.org/">MetaCPAN</a>. It does fight the principal of DRY, or, in this case &#8220;do not commit generated files&#8221; but it could be the lesser evil.</p>

<p>I have lately learned that <a href="https://devin.ai/">Devin, the AI software engineer</a> is being used to create summaries and presentations of GitHub repositories in <a href="https://deepwiki.com/">DeepWiki</a>. For an example of a Perl project, my <a href="https://deepwiki.com/mikkoi/env-assert">Env-Assert</a>.</p>
