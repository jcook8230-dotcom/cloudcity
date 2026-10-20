We have our repo prepared, two files created and two commits done. Let's see how it looks.

`cd test`

`git status`

`git log`

Let's move ourselves back by one commit.

`git revert --no-edit HEAD`

We succesfully moved back by creating new commit.

`git log`

By using `--no-edit` we informed git that we don't want to pass any message and we ask to use default. We will see what git did for us, using `git log` soon.

So, now we are back one commit from two already done and... we have three commits. Strange? Please, try to think about the logic behind. We do not want to create problems for other users which can work on the same repo with us. So, we 'go back by going forward'. We keep the history and logic process of work, however we bring back the part of the work from kind of 'backup'.

Our current status is like this: we are between two commits, for file-01 and file-02.

Let's have some fun, and revert our revert. Shall we?

`git revert --no-edit HEAD`

Before you run next commad, please try to imagine what happened in our git :)

`git log`

Of course, we can revert more changes than the last commit.

We can revert multiple commits by

`git revert --edit HEAD~3`

This time we reverted to the beginning of our history. And we forced git to give us possibility to add message (by the way, `--edit` is default behavior).

So, to make sure we all are on the ame page. `HEAD` is the current 'place' where we are. For now, let's think about it as combination of current branch and current place in git history.

So, with `HEAD~3` we said: `I want to move back from HEAD by 3 commits` . But that's not all. This place becomes our new `HEAD` .

We can revert to specific commit hash too. more about hashes in `git log` scenario.