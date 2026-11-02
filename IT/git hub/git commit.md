Then let's focus on commit. Once that clicks, push is just "send it."

## What a commit is

A commit is a **saved snapshot** of your staged changes, with a label (the message). It's like a save point in a game: you can always go back to it and see what changed.

Before you can commit, you have to **stage** (with `git add`) what goes into the snapshot. The commit only includes what's staged.

```
 edit file  ──►  git add  ──►  git commit -m "msg"  ──►  git push
 (changed)      (staged)       (snapshot saved          (snapshot sent
                                on your computer)        to GitHub)
```

## The command

```bash
git commit -m "your message here"
```

- **`commit`** = take the snapshot
- **`-m`** = "here's my message"
- **`"..."`** = the label, in quotes

Without `-m`, git opens a text editor and asks for the message, which can be confusing. Always use `-m` for now.

## Writing a good message

Describe **what you changed**, short and in present tense:

|Good ✅|Not helpful ❌|
|---|---|
|`"Add run 3 notes"`|`"stuff"`|
|`"Fix typos in lab1 notes"`|`"update"`|
|`"Add lesson1 screenshots for runs 1-7"`|`"asdf"`|

_Test:_ if you read the message a month from now, would you know what the commit did?

## How to tell whether a commit worked

After `git commit`, you'll see something like:

```
[main 3f2a1b9] Add run 3 notes
 1 file changed, 2 insertions(+)
```

- `3f2a1b9` = the commit's short ID
- `1 file changed` = what went into the snapshot

Then `git status` will say **"ahead of 'origin/main' by 1 commit"**, which means the commit is saved locally and ready to push.