We have repo prepared. changes are done and commited. And one file is updated again.

Before we start, we have to change the work directory.

`cd test`

`git status`

`git log`

Another command, `git diff`, allows to check the differences between `HEAD` and current working directory. Another words, what was changed during our recent work.

`git diff`

As usual, this command checks HEAD by default. However, we can modify it.

`clear && git diff HEAD~1`

As you can expect, when we go deeper into past, more information is printed. If we want to avoid the mess, we can check diff for one file.

`clear && git diff HEAD~1 testfile-01`

Now we see information about `testfile-02` only in comparision of current working directory and one commit before HEAD.# 

Staged differences

We already learned that `git diff` shows differences between commit and working directory. So, what about staged changes?

Let's test

`touch testfile-03 && echo "testfile-03" > testfile-03 && git add testfile-03`

We created a new file and added it to staging. now let's see the difference between the current working directory and HEAD.

`git diff`

Well, there is nothing about our new file.

In order to see the difference between staged work and HEAD, you need to say this explicitly.

`git diff --staged`

Git show
Another useful commad is git show. This will give you information similar to git log.

git show work by default against HEAD. Of course you can use it to any commit and any file.

git show