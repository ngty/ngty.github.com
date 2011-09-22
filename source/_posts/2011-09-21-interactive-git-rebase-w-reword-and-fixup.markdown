---
layout: post
title: "Interactive Git Rebase With Reword &amp; Fixup"
date: 2011-09-21 20:32
comments: true
categories: 
- git
- tips
---

It is no secret that i'm a fan of interactive git rebase. It gives me
the power to clean up the numerous small intermediate commits that i
did so frequently while in the course of completing a feature (or bugfix).
In the process, i usually do quite abit of squashing, reshuffling &
rewording, such that the eventual commits i push upstream are
well-organized & each commit is meaningful to the rest of the team.

Usually i use `pick` & `squash` to achieve the compressing of different
commits. Recently, my coworker showed me an alternative, which uses `reword`
& `fixup`.  Here's how it can be done:

{% codeblock %}
$ git rebase -i <branch>
{% endcodeblock %}

Instead of doing:

{% codeblock %}
pick 6354612 WIP ~ monkey patched to fix bug#234.
squash 4de4f66 WIP ~ conform to recommended way of patching.
squash 3545b15 WIP ~ fixed incomplete removal of hackish patch.
squash 7000cfe WIP ~ removed the no-longer-needed :rightnow tag.
{% endcodeblock %}

Do this:

{% codeblock %}
reword 6354612 WIP ~ monkey patched to fix bug#234.
fixup 4de4f66 WIP ~ conform to recommended way of patching.
fixup 3545b15 WIP ~ fixed incomplete removal of hackish patch.
fixup 7000cfe WIP ~ removed the no-longer-needed :rightnow tag.
{% endcodeblock %}

Of course, the 2 approaches are different:

- `reword` & `fixup`, u get to either keep the 1st commit message,
or rephrase it
- `pick` & `squash`, u have more choices ~ from keeping all of the
various commit messages, to writing a brand new message

For me, i almost always want the effect of `reword` & `fixup`.
