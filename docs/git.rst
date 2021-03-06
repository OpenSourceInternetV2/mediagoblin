==========================
 Git, Cloning and Patches
==========================

.. contents:: Sections
   :local:


GNU MediaGoblin uses git for all our version control and we have the
repositories hosted on `Gitorious <http://gitorious.org/>`_.  We have
two repositories:

* MediaGoblin software: http://gitorious.org/mediagoblin/mediagoblin
* MediaGoblin website: http://gitorious.org/mediagoblin/mediagoblin-website

It's most likely you want to look at the software repository--not the
website one.

The rest of this chapter talks about using the software repository.


How to clone the project
========================

Do::

    git clone git://gitorious.org/mediagoblin/mediagoblin.git


How to contribute changes
=========================

Tie your changes to issues in the issue tracker
-----------------------------------------------

All patches should be tied to issues in the `issue tracker
<http://bugs.foocorp.net/projects/mediagoblin/issues>`_.  That makes
it a lot easier for everyone to track proposed changes and make sure
your hard work doesn't get dropped on the floor!  If there isn't an
issue for what you're working on, please create one.  The better the
description of what it is you're trying to fix/implement, the better
everyone else is able to understand why you're doing what you're
doing.


Use bugfix branches to make changes
-----------------------------------

The best way to isolate your changes is to create a branch based off
of the MediaGoblin repository master branch, do the changes related to
that one issue there, and then let us know how to get it.

It's much easier on us if you isolate your changes to a branch focused
on the issue.  Then we don't have to sift through things.

It's much easier on you if you isolate your changes to a branch
focused on the issue.  Then when we merge your changes in, you just
have to do a ``git fetch`` and that's it.  This is especially true if
we reject some of your changes, but accept others or otherwise tweak
your changes.

Further, if you isolate your changes to a branch, then you can work on
multiple issues at the same time and they don't conflict with one
another.


Properly document your changes
------------------------------

Include comments in the code.

Write comprehensive commit messages.  The better your commit message
is at describing what you did and why, the easier it is for us to
quickly accept your patch.

Write comprehensive comments in the issue tracker about what you're
doing and why.


How to send us your changes
---------------------------

There are two ways to let us know how to get it:

1. *(preferred)* **push changes to publicly available git clone and
   let us know where to find it**

   Push your feature/bugfix/issue branch to your publicly available
   git clone and add a comment to the issue with the url for your
   clone and the branch to look at.

2. **attaching the patch files to the issue**

   Run::

       git format-patch --stdout <remote>/master > issue_<number>.patch
       
   ``format-patch`` creates a patch of all the commits that are in
   your branch that aren't in ``<remote>/master``.  The ``--stdout``
   flag causes all this output to go to stdout where it's redirected
   to a file named ``issue_<number>.patch``.  That file should be
   based on the issue you're working with.  For example,
   ``issue_42.patch`` is a good filename and ``issue_42_rev2.patch``
   is good if you did a revision of it.

   Having said all that, the filename isn't wildly important.


Example workflow
================

Here's an example workflow.


Contributing changes
--------------------

Slartibartfast from the planet Magrathea far off in the universe has
decided that he is bored with fjords and wants to fix issue 42 (the
meaning of life bug) and send us the changes.

Slartibartfast has cloned the MediaGoblin repository and his clone
lives on gitorious.

Slartibartfast works locally.  The remote named ``origin`` points to
his clone on gitorious.  The remote named ``gmg`` points to the
MediaGoblin repository.

Slartibartfast does the following:

1. Fetches the latest from the MediaGoblin repository::

       git fetch --all -p

   This tells ``git fetch`` to fetch all the recent data from all of
   the remotes (``--all``) and prune any branches that have been
   deleted in the remotes (``-p``).

2. Creates a branch from the tip of the MediaGoblin repository (the
   remote is named ``gmg``) master branch called ``bug42_meaning_of_life``::

       git checkout -b bug42_meaning_of_life gmg/master

   This creates a new branch (``-b``) named ``bug42_meaning_of_life`` based
   on the tip of the ``master`` branch of the remote named ``gmg`` and checks
   it out.

3. Slartibartfast works hard on his changes in the ``bug42_meaning_of_life``
   branch.  When done, he wants to notify us that he has made changes
   he wants us to see.

4. Slartibartfast pushes his changes to his clone::

       git push origin bug42_meaning_of_life --set-upstream

   This pushes the changes in the ``bug42_meaning_of_life`` branch to the
   remote named ``origin``.

5. Slartibartfast adds a comment to issue 42 with the url for his
   repository and the name of the branch he put the code in.  He also
   explains what he did and why it addresses the issue.


Updating a contribution
-----------------------

Slartibartfast brushes his hands off with the sense of accomplishment
that comes with the knowledge of a job well done.  He stands, wanders
over to get a cup of water, then realizes that he forgot to run the
unit tests!

He runs the unit tests and discovers there's a bug in the code!

Then he does this:

1. He checks out the ``bug42_meaning_of_life`` branch::

       git checkout bug42_meaning_of_life

2. He fixes the bug and checks it into the ``bug42_meaning_of_life`` branch.

3. He pushes his changes to his clone (the remote is named ``origin``)::

       git push origin bug42_meaning_of_life

4. He adds another comment to issue 42 explaining about the mistake
   and how he fixed it and that he's pushed the new change to the
   ``bug42_meaning_of_life`` branch of his publicly available clone.


What happens next
-----------------

Slartibartfast is once again happy with his work.  He finds issue 42
in the issue tracker and adds a comment saying he submitted a merge
request with his changes and explains what they are.

Later, someone checks out his code and finds a problem with it.  He
adds a comment to the issue tracker specifying the problem and asks
Slartibartfast to fix it.  Slartibartfst goes through the above steps
again, fixes the issue, pushes it to his ``bug42_meaning_of_life`` branch and adds
another comment to the issue tracker about how he fixed it.

Later, someone checks out his code and is happy with it.  Someone
pulls it into the master branch of the MediaGoblin repository and adds
another comment to the issue and probably closes the issue out.

Slartibartfast is notified of this.  Slartibartfast does a::

   git fetch --all

The changes show up in the ``master`` branch of the ``gmg`` remote.
Slartibartfast now deletes his ``bug42_meaning_of_life`` branch
because he doesn't need it anymore.


How to learn git
================

Check out :ref:`hacking-howto-git`!
