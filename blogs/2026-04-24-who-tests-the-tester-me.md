---
title: "Who tests the tester? Me !!!"
url: "https://blogs.perl.org/users/lichtkind/2026/04/who-tests-the-tester-me.html"
date: "2026-04-24T19:21:07Z"
author: "lichtkind"
feed_url: "https://blogs.perl.org/atom.xml"
---
<p>As <a href="https://blogs.perl.org/users/lichtkind/2026/03/graphicstoolkitcolor-20-feater-overview.html">already reported</a>, I'm writing this <a href="https://metacpan.org/pod/Graphics::Toolkit::Color">color library</a>. Recently I created my own test function for it. And since it was easier that I thought, I want to show you how, so you can write your own!</p>

        <p><strong><big>The Task</big></strong></p>

<p>If you look into the <a href="https://blogs.perl.org/users/lichtkind/2025/08/architecture-of-gtc-18.html">GTC internals</a>, you see instantly that the most common none OO data structure is a <em>'tuple'</em> with the values of one color in one color space (usually three values). Since we do not have a native tuple type in Perl - it is an ordinary Array, one could  also say a value vector. In the GTC test suite they get checked very often. Each time I have to ask:</p>

<ol>
    <li>Did I get an Array ?</li>
    <li>Does it have the right amount of values ?</li>
    <li>Check every value of the tuple for equality.</li>
</ol>

<p>These are usually 5 lines that could and should have been one line. In practice this means 200 rows of test code will shrink to 40 - neat. Less to type, less to read - wonderful.  And the assertions will be more to the point telling WHAT I want to test and WHY not just two values match, which is also good for readability and clarity on the other end. If running the tests, the <em>ok</em> - messages will tell me what is actually tested and not that two values matched. But the most important improvement comes to light when something goes wrong. Let's say the function we test collapses and returns <em>undef</em>. The first test will tell us that we got no ARRAY, good, but the next who checks the lengths of the array will crash in a hard syntax error. You have to fix the causing bug in order to see the next test results because your test suite crashed. Wouldn't it be so much nicer the test suite could run to the end and the error messages tell you about all the bugs at once, so you could theoretically hunt them in one go.</p>

<p>You see: less code, clearer code, better error message, only relevant error messages and no hard crashes. These are more than enough motivating reasons to write custom error functions, so let's do it, let's write a variant of </p>

<pre><code>is( $got, $expected, $test_name );
</code></pre>

<p>(which is a test function you all used at some point) and name it:</p>

<pre><code>is_tuple( $got, $expected, $axis, $test_name );
</code></pre>

<p>You notice I needed one more argument for the axis names. So I can get the nice error message: "the red value was 13 but I expected 15".</p>

<p><strong><big>The Solution</big></strong></p>

<p>The Module you need to create that is <a href="https://metacpan.org/pod/Test::Builder">Test::Builder</a>. So the smart ones among you have guessed you need to:  </p>

<pre><code>use Test::Builder;
my $tb = Test::Builder-&gt;new;
</code></pre>

<p>You can also subclass Test::Builder but this works as well, since ->new will give you the only instance of $tb anyway. And to start our test function we need just:</p>

<pre><code>sub is_tuple {
my ($got, $expected, $axis, $name) = @_;
my $pass = 0;
my $diag = '';
</code></pre>

<p>Well if you are reading this blog, you know about Perl argument handling. $pass is the pseudo boolean than holds the information if the test was successful, we pass it on to the Test::Builder method at the end. Same is true for $diag, which is the error message we maybe have to drop. This is not the way you have to do it. Calling the diag method several times is also an option, but i prefer to have short error messages that fits in one line and only tells me what exactly went wrong. Let's skip the testing logic, since a bunch of nested if statements with some basic value checks isn't that impressive and educational. I just like a clean separation between out test logic and the part where I talk to Test::Builder. That is why I declared the variables at the start, fill them when i need to, so I only call the following once at the end of the subroutine:</p>

<pre><code>$tb-&gt;diag( $diag ) unless $pass;
$tb-&gt;ok( $pass, $name );
</code></pre>

<p>Yes that is all. Do not forget to:</p>

<pre><code>require Exporter;
our @ISA = qw(Exporter);
our @EXPORT = qw(is_tuple);
</code></pre>

<p>But this was really it. It didn't even hurt and we didn't have to see Detroit.</p>

<p><strong><big>The Tests</big></strong></p>

<p>More challenging I found it to write the test file that checks the logic code I didn't show in the above example.</p>

<pre><code>use v5......;
use warnings;
use lib '.',...;
use Test::More tests =&gt; ...;
use Test::Builder::Tester;
use Test::Color;
</code></pre>

<p>This is mostly your usual start template of any test file. The <em>lib</em> pragma needs to receive the directory where the module lives, that contains <em>is_tuple</em>, which would be in my case Test::Color. And we need <a href="https://metacpan.org/pod/Test::Builder::Tester">Test::Builder::Tester</a> to test what we built with Test::Builder (the module names fit).</p>

<pre><code>test_out("ok 1 - is_tuple runs");
is_tuple([1,1,1], [1,1,1], [qw/red green blue/], 'is_tuple runs');
test_test("simplest is_tuple case runs");
</code></pre>

<p>Our first little smoke test seems trivial. We call <em>is_tuple</em> with the the result values of some operation (<em>$got</em>) and the values to check them against (<em>$expected</em>), then the axis names and at last the test name (the name of the test is_tuple performs). But BEFORE that you HAVE TO tell Test::Builder::Tester what output to expect from the test function <em>is_tuple</em> on STDOUT. The last line tells Test::Builder::Tester the name of the test we did by testing the test function. That HAS to come AFTER calling <em>is_tuple</em>.</p>

<p>Now we are ready for the juicy bit. How to test a failing test? I mean by that: <em>is_tuple</em> will fail because we gave it bad data by purpose. And if <em>is_tuple</em> tries to give the right error message to STDERR (standard error output), Test::Builder::Tester should intervene and call it a successful test to STDOUT. The code to do this is:</p>

<pre><code>test_out("not ok 1 - C");
test_err("# failed test: C - got values that are not a tuple (ARRAY ref)");
test_fail(+1);
is_tuple(1, [1,1,1], [qw/red green blue/], 'C');
test_test("is_tuple checks if got values in an ARRAY");
</code></pre>

<p>First we tell via <em>test_out</em> again what STDOUT suppose to receive. Then we tell via <em>test_err</em> what error message should land in STDERR. And when a test fails Test::Builder will create an additional error message telling where it happened. In order to not have to chase line numbers we got the convenience function:  <em>test_fail(+1);</em> You can translate it to: "Hej Test::Builder::Tester, the next line (+1) will cause an error, this is fine, please do not create this additional error with the line number". What actually happens is, this call gets forwarded to a <em>test_err</em> call with the appropriate string that contains the right line number. Then we finally call the test function we want to test and at the very end again - the name of this (meta) test.</p>

<p>One last useful hack. You noticed I called the test that <em>is_tuple</em> does in the last example  just uppercase C. This is not a nice and telling name for any test and brutally counterproductive - However - since we testing the test and the name of the inner test is part of the STDOUT and STDERR check string in the outer test, it is nice to trace easily what substring comes from where and this is also rather educational for this demo. What this (inner) test suppose to do is documented anyway by the name of the outer test. </p>
