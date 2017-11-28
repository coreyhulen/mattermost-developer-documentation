---
draft: true
title: "Contribution Guidelines"
date: 2017-08-20T12:33:36-04:00
weight: 1
subsection: Getting Started
---

<div class="section" id="code-contribution-guidelines">
<span id="code-contribution-guidelines"></span><h1>Contribution Guidelines</h1>
<p>Thank you for your interest in contributing to Mattermost. To help with translations, <a class="reference external" href="https://docs.mattermost.com/developer/localization.html">see the localization process</a>. For code contributions, here's the process:</p>
<div class="section" id="choose-a-ticket">
<span id="choose-a-ticket"></span><h2>Choose a Ticket</h2>
<ol class="simple">
<li>Choose a ticket from the <a class="reference external" href="https://github.com/mattermost/platform/issues?utf8=%E2%9C%93&amp;q=is%3Aissue%20is%3Aopen%20%5BHelp%20Wanted%5D">Help Wanted GitHub Issues</a> list.<ul>
<li>Make sure that it doesn't have an <a class="reference external" href="https://github.com/mattermost/platform/pulls">open pull request</a> for it.</li>
</ul>
</li>
<li>Before starting to work on the ticket, comment to let people know you're working on it.</li>
<li>If you have questions, post them in <a class="reference external" href="http://forum.mattermost.org/">Mattermost forum</a> or join the <a class="reference external" href="https://pre-release.mattermost.com/core/channels/tickets">Contributors</a> channel and announce the ticket you'd like to work on so it can be assigned to you.</li>
</ol>
<p>It is fine to submit a PR for a bug or an incremental improvement with less than 20 lines of code change without a Help Wanted issue if the change to existing behaviour is small. Some examples include</p>
<ul class="simple">
<li><a class="reference external" href="https://github.com/mattermost/platform/pull/5640">Fix a formatting error in help text</a></li>
<li><a class="reference external" href="https://github.com/mattermost/platform/pull/5809">Fix success typo in Makefile</a></li>
<li><a class="reference external" href="https://github.com/mattermost/platform/pull/5612">Fix broken Cancel button in Edit Webhooks screen</a></li>
<li><a class="reference external" href="https://github.com/mattermost/mattermost-mobile/pull/364">Fix Android app crashing when saving user notification settings</a></li>
<li><a class="reference external" href="https://github.com/mattermost/platform/pull/5878">Fix recent mentions search not working</a></li>
</ul>
<p>Core committers who review the PR are entitled to reject the PR if it significantly changes behavior or user expectations, which <a class="reference external" href="http://docs.mattermost.com/process/help-wanted.html">requires a Help Wanted issue opened by the core team</a> so that the change can be tested, documented and supported.</p>
<p>The best way to discuss opening a Help Wanted ticket with the core team is by <a class="reference external" href="https://www.mattermost.org/feature-ideas/">starting a conversation in the feature idea forum</a>.</p>
</div>
<div class="section" id="install-mattermost-and-set-up-a-fork">
<span id="install-mattermost-and-set-up-a-fork"></span><h2>Install Mattermost and set up a Fork</h2>
<p>Once you have a ticket:</p>
<ol class="simple">
<li>Follow the <a class="reference external" href="/contribute/getting-started/developer-setup/">developer setup instructions</a> to install Mattermost.</li>
<li>Create a branch with <code class="docutils literal"><span class="pre">&lt;branch</span> <span class="pre">name&gt;</span></code> set to the ID of the ticket you're working on, for example <code class="docutils literal"><span class="pre">PLT-394</span></code>, using the command: <code class="docutils literal"><span class="pre">git</span> <span class="pre">checkout</span> <span class="pre">-b</span> <span class="pre">&lt;branch</span> <span class="pre">name&gt;</span></code></li>
<li>Take a look at the <a class="reference external" href="https://docs.mattermost.com/developer/developer-flow.html">developer flow</a> to learn how to work with the Mattermost codebase.</li>
</ol>
</div>
<div class="section" id="preparing-a-pull-request">
<span id="preparing-a-pull-request"></span><h2>Preparing a Pull Request</h2>
<p>Before submitting a pull request (PR), check that:</p>
<ol class="simple">
<li>You’ve signed the <a class="reference external" href="http://www.mattermost.org/mattermost-contributor-agreement/">Contributor License Agreement</a>, so you can be added to the Mattermost <a class="reference external" href="https://docs.google.com/spreadsheets/d/1NTCeG-iL_VS9bFqtmHSfwETo5f-8MQ7oMDE5IUYJi_Y/pubhtml?gid=0&amp;single=true">Approved Contributor List</a>.</li>
<li>Your change has a <a class="reference external" href="http://docs.mattermost.com/process/help-wanted.html">Help Wanted ticket</a></li>
<li>Your code follows the <a class="reference external" href="http://docs.mattermost.com/developer/style-guide.html">Mattermost Style Guide</a>.</li>
<li>Unit tests are included for new server side functionality.</li>
<li>Strings in user interface are included in <a class="reference external" href="https://github.com/mattermost/platform/blob/master/i18n/en.json">.../i18n/en.json</a> and <a class="reference external" href="https://github.com/mattermost/platform/tree/master/webapp/i18n/en.json">.../webapp/i18n/en.json</a> localization files. Files for other languages will automatically be updated through the <a class="reference external" href="http://translate.mattermost.com">Mattermost Translation Server</a> and do not need to be included in the pull request.</li>
<li>Change meets UX Guidelines of <a class="reference external" href="http://www.mattermost.org/design-principles/">Fast, Obvious, Forgiving</a>.</li>
<li>If change requires user to understand a new concept or make a decision, PR for help documentation is submitted to <a class="reference external" href="https://github.com/mattermost/docs">mattermost/docs</a>.</li>
<li>Change is thoroughly tested. If your change involves text processing, make sure to at least run markdown loadtests in <a class="reference external" href="https://github.com/mattermost/platform/tree/master/tests"><code class="docutils literal"><span class="pre">/tests</span></code></a> before submitting the PR. To run the loadtests:<ul>
<li>Go to <strong>System Console</strong> &gt; <strong>Developer</strong> and set <strong>Enable Testing Commands</strong> to true</li>
<li>Run <code class="docutils literal"><span class="pre">/test</span> <span class="pre">url</span> <span class="pre">test-markdown-basics.md</span></code> and follow the instructions</li>
<li>Run <code class="docutils literal"><span class="pre">/test</span> <span class="pre">url</span> <span class="pre">test-markdown-lists.md</span></code> and follow the instructions</li>
<li>Run <code class="docutils literal"><span class="pre">/test</span> <span class="pre">url</span> <span class="pre">test-tables.md</span></code> and follow the instructions</li>
</ul>
</li>
<li>Confirm you have <a class="reference external" href="http://git-scm.com/book/en/v2/Git-Tools-Rewriting-History#Squashing-Commits">squashed your commits</a>.</li>
</ol>
</div>
<div class="section" id="submitting-a-pull-request">
<span id="submitting-a-pull-request"></span><h2>Submitting a Pull Request</h2>
<p>When submitting a PR, check that:</p>
<ol class="simple">
<li>PR is submitted against <code class="docutils literal"><span class="pre">master</span></code></li>
<li>PR title begins with the Jira Ticket ID (eg <code class="docutils literal"><span class="pre">PLT-394:</span></code>, <a class="reference external" href="https://github.com/mattermost/platform/pulls?q=is%3Apr+is%3Aclosed">see examples</a>)</li>
<li>PR comment describes the changes and how the feature is supposed to work</li>
</ol>
</div>
<div class="section" id="managing-an-open-pull-request">
<span id="managing-an-open-pull-request"></span><h2>Managing an Open Pull Request</h2>
<p>After submitting a PR, before it is merged:</p>
<ol class="simple">
<li>Automated build process must pass<ul>
<li>If the build fails, check the error log to narrow down the reason.</li>
<li>Sometimes one of the multiple build tests will randomly fail due to issues in Travis CI. If you see just one build failure and no clear error message, it may be a random issue. Add a comment so the reviewer for your change can re-run the build for you, or close the PR and re-submit and that typically clears the issue.</li>
</ul>
</li>
<li>PM review must pass<ul>
<li>A Product Manager will review the pull request to make sure it:<ul>
<li>Fits with our product roadmap</li>
<li>Works as expected</li>
<li>Meets <a class="reference external" href="https://docs.mattermost.com/developer/fx-guidelines.html">UX guidelines</a></li>
</ul>
</li>
<li>The Product Manager may come back with some bugs or UI improvements to fix before the pull request moves on to dev review.</li>
</ul>
</li>
<li>CSS review must pass<ul>
<li>Any pull request containing CSS changes should be reviewed by the UX and HTML/CSS dev.</li>
</ul>
</li>
<li>Dev review must pass<ul>
<li>Two core committers will review the pull request and either give feedback or approve the PR.</li>
<li>Any comments will need to be addressed before the pull request is ready to merge.</li>
</ul>
</li>
</ol>
<p>If you've included your mailing address in the signed <a class="reference external" href="https://www.mattermost.org/mattermost-contributor-agreement/">Contributor License Agreement</a>, you may receive a <a class="reference external" href="https://forum.mattermost.org/t/limited-edition-mattermost-mugs/143">Limited Edition Mattermost Mug</a> as a thank you gift after your first pull request is merged.</p>
</div>
</div>
