---
layout: post
title:  "Splitting Git Commits"
date:   2017-12-20 14:00:00 +0200
tags:   git rewrite history
---

Change your commit history is not something to do under normal development, but it can be an extremely valuable tool while doing change set management. It helps keeps a commit history (a change set list) clean and managable. A clean history enables easy cherry-picking of commits if you are maintaining multiple branches or versions.

Here's an example of how to split a mega-commit into multiple smaller commits. The tools we are going to use are

* ``git rebase`` (changing history)
* ``git reset`` (for undoing commits)
* ``git stash`` (for managing unwanted changes)

The general approach we are going to follow is:

1. Rebase to edit the history
2. Rollback mega-commit
3. Repeatedly apply smaller commits while testing each commit.

Before starting I always ensure that the working directory is clean, with no
uncommit changes and no untracked files.

The first step is to initiate the rebase. Rebase can be used to move a branch up
on a new baseline (upstream), but you can also use it to edit the history while
keeping the baseline the same. We will use the ``--interactive`` option to
specify that we want to change things around. The upstream version in this case
will be the newest commit we want to leave unchanged and keep as the base
version for our new history. Find the commit id of this commit in the history
and start the rebase:

    git rebase --interactive <upstream>

Now we will change the rebase operation of one (or more) commits. To split a
commit we will need to change the operation of those commits to 'edit'.

When the rebase operation reaches the commit we want to edit, it will drop into
the command prompt. It has already applied the commit, so to change it we will first undo it:

    git reset HEAD~

This will remove the commit, move ``HEAD`` back to the previous commit
(``HEAD~``) while leaving all the changes of the commit in the working
directory.

Now we can be commiting the individual changes we want. I use ``git add`` to add
indivial files and ``git add --patch`` to selectively add invidual changes. If a
change is completely interleaved, the patch can be edited directly while doing
``git add --patch``.

Before we commit the partial change, we might want to check if it can be built
and verify that the unit tests pass. Currently we still have all the changes in
the working directory, so lets get rid of those using ``git stash``:

    git stash --keep-index --include-untracked

Now all our changes (except those we added to the index using ``git add``) are
in the stash and have been removed from the working directory. ``--keep-index``
ensures that all the changes we added are not also stashed (stash's default
behaviour). ``--include-untracked`` push all untracked files into the stash as
well.

After building and testing, we can commit our change. If there were any
problems, we can apply our stashed changes (``git stash apply``) and repeated
our selective addition of changes to the index.

    git commit

Followed by reapplying our changes remaining in the stash:

    git stash apply

At this point we are back with a set of changes in the working directory, but
with a new commit in the history containing some of the changes. We can either
commit the rest in one go, or repeat partial commits using this procedure.

When everything has been commited, we can continue the rebase:

    git rebase --continue

As a final sanity check, we can compare our resulting state of the tree with
what we had before the rebase. For this we need the commit ID of the HEAD commit
before we started the rebase (find using ``git reflog``).

    git diff <commit id>

If you correctly applied all the changes and didn't discard any changes, this
output should be completely empty.
