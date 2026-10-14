`hooks` directory contains all custom hooks. These are small (usually) scripts which have to be executed before commit, or after, before push, etc.

`branches` - this is deprecated. Don't think about it anymore.

`HEAD` - pointer to the current branch and its latest commit.

`config` - configuration file for the repository.

`info` - the place where you stage the files using `git add`.

`refs` - the current state of the whole repo.

`objects` - commits, trees and blobs are stored here. May be very big.

`logs` - quite self explanatory.

`description` - description of the repository.

how to remove files from commit 
git rm --cached 
`git rm --cached -r .`

please notice, we used `.` to say `everything from here` and `-r` which means `recursive`.

`git log`

About git log we will talk in another scenario.

Also, you can see some modifications were done in files after previous commit.

We have all 4 files ready to be commited, but unfortunately, we don't want those changes.

First, let's check what is in the file `testfile-01`

`cat testfile-01`

`git checkout testfile-01`

`cat testfile-01`

`git status`

We succesfully reset the file to the state from previous commit, using `git checkout`. In this way we do the `checkout` of the last indexed state of this file on current branch.

In similar way like in some scenarios before, we can remove all changes in one short command. Let's do it.

`git checkout .`

`git status`
# Reset the current HEAD to the selected state

`git reset` moves the current pointer in `HEAD` and `branch refs` to specific state. `git checkout` does similar thing, but in fact, both of these commands operates on different levels. This theory will be explained later.

`Reset` has three main ways of operating, but we will touch only two of them. This time `--mixed` is not covered.

## --soft

`git log` shows that we have many changes done. We have one commit for each file.

`git log`

Let't reset the HEAD to the state before commiting the last file.

But before, let's see what is inside the files

`cat testfile-04`

`cat testfile-02`

`git reset --soft HEAD~1`

Now let's see what we have.

`git status`

`git log`

`cat testfile-04`

With `--soft` parameter we came back to the previous HEAD of the repository, but all changes which we commited are unchanged.

## --hard

Now let's try something more powerful.

`git reset --hard HEAD~2`

And let's look what happened

`git status`

`git log`

`cat testfile-04`

`cat testfile-02`

What we did?

We came back two more commits (~HEAD~2) and we said, this time we want to not only move back, but also we want to remove all changes which were done.