Contributing to Gem development
====

Gem-development is quite short on manpower.
So if you want to contribute, you are very welcome.

# What can you do

 - fix bugs
 - implement features
 - write help-patches
 - write documentation
 - provide nice examples
 - ...

# Communication

## Mailinglist

Virtually all communication regarding the development of Gem, happens on the
[Gem-dev mailinglist](http://lists.puredata.info/listinfo/gem-dev).

If you want to contribute, you are invited (and urged :-)) to join the mailinglist.

## Issues

Issues are collected online in several issue-trackers:

- [Github issues](https://github.com/umlaeute/Gem/issues) - mainly targeted at the development process
- [Bugs](https://sourceforge.net/p/pd-gem/bugs) (SourceForge) - this is where most end-users report their problems
- [Feature Requests](https://sourceforge.net/p/pd-gem/feature-requests) (SourceForge) - this is where most end-users report their feature requests



# Getting your changes into Gem


## Version Control System
Gem uses `git` for source code management.
the official public repository is on github:
   https://github.com/umlaeute/Gem
a secondary repository is on sourceforge:
   git://git.code.sf.net/p/pd-gem/gem


## preparing your changes
If you want to contribute, please make sure that your changes can be
applied to the latest HEAD (which might be slightly different from the one
when you started working on your contribution).

### git commits
**commit often!**

We want to be able to track down a bug to the very commit it was introduced.
If a single commit does numerous unrelated things, it makes finding the bug unnecessary complicated.

Committing properly, eases review, cherry picking, bisecting (and thus debugging) and backporting

Here are a few rules that should help to make good commits:

#### incremental commits
Each commit should be a *small* and *incremental* change to the codebase.

#### One change per commit.
Please break your commit into *sensible* chunks.
A sensible chunk only does a single thing (e.g. "fix bug #666", or "proper indentation").
If you have fixed two bugs in a single file, it's probably good to make this *two separate* commits.
Even if each commit only changes a single line.
OTOH, a sensible chunk *can* (and often does) spread over multiple files.
E.g. if you have added a new feature by adding a new method to an object, this most often means that
you had to edit both the header and the implementation file for this object.
The changes to both files belong together and therefore should go into a single commit.

#### mixing file types

Avoid committing Pd-patches and C++ code within the same commit.
Conflicts in C++-code can usually easily be resolved,
whereas conflicts in Pd-patches are usually impossible to resolve (but for the most trivial cases).

#### binary data

Do *not* add binary data to the git repository (without a consensus on gem-dev first).
Not even temporarily!

### git branching
Try to avoid forking from branches other than master.
Esp. avoid branches on top of branches.
Before committing a pull request, make sure that your branch applies clean to current master.


## Workflows
I try to enforce a git-based workflow even for simple commits for various reasons.

One of them is *proper attribution*: if you have made a contribution,
you should also appear as the author of this contribution (e.g. in the version history).
Rather than somebody who happens to have commit rights on the repository.

### Github workflow
The preferred way for contributing is by forking the github repository
and creating a pull request once your code is ready.

### other workflow
If you do not want to create an account on github, this is fine as well.
Just clone the repository, and email the patch-set (e.g. via the mailing list).
e.g.

    $ git clone https://github.com/umlaeute/Gem.git
    $ cd Gem
    $ git checkout -b nifty_feature
    // now fix a bug
    $ git commit -m "fixed crasher bug"
    // now add a feature
    $ git commit -m "made zgonc work"

    $ git format-path master/origin
    // this will create a number of .patch files
    // zip them, and send them to me
    $ tar cvzf /tmp/nifty_feature.tgz *.patch

Alternatively you can also use `git send-email` tor automatically sending the patch-set as multiple emails.

# Coding Style

Gem's Coding style is not very formalized.
However, there are some implicit assumptions.

There is a [draft document](https://github.com/umlaeute/Gem/blob/master/doc/CodingStyle.txt)
that tries to sum up the current practice.


# Questions?

If you still have questions, please ask them on the gem-dev mailinglist:
   http://lists.puredata.info/listinfo/gem-dev
