# Formatting information from git log

Right now we know how `git log` works. Well, it is ok, but is there any way to extract some data or format messages? Or even query them?

Yes!

**Remember to quit `git log` with `q`. If logs are longer than your screen, it always goes to interactive mode.**

We have repo prepared. Some work was done. Even one revert was executed.

`git log` shows it pretty well. But imagine, how it will look with thousands of commits?

## Best for programmatic access

Sometimes you want to check commits through scripts. In this case `git log` itself is unhandy. What to do to have it better formatted for scripts?

`cd test && clear && git log --oneline`

`--oneline` shows only most important info about commits. You have only hash and commit message.

Is this enough? We can argue. But definitely is more clear for high level understanding of previous work. How to make it better we will see soon.

Let's clear our screen

`clear`

Do you remember the

`git show` command?

It shows more details about last (or selected) commit.

But hey! We can do this for all commits!

`clear && git log -p`

Please remember to use `q` key to escape and come back to shell.

Some statistics' folks wish to know what amount of work was done in the commit. Git gives this possibility

`clear && git log --stat`

Now we can clearly see how many lines were added or removed in each commit.

Maybe you wish to see the information sorted by author of the commits?

`clear && git shortlog` is the answer!

# Prettier output?

Let's `clear` the screen first.

Ok, we know how to do some basics tricks. But maybe we want to visualize some work with branches, etc?

`git log --graph`

You can clearly see that in some moment we created another branch, we did some work there and then we merged it (branches will be described soon)

But... It doesn't look good, doesn't it?

Git gives us the possibility to connect multiple parameters in one command.

`clear && git log --oneline --graph`

# Formatting

Git allows us to use special formatting to print exactly what we want.

Sometimes your log is very plain. If this is your case and you would like to have more colorful output, use `--decorate` parameter.

A few examples which we combine into a working command:

`%Cblue` - switch output text to blue

`%Creset` - resets the color to default

`%H` - commit hash. Preferable is to use short hash with `%h`.

`%an` - who commited the changes

`%ad` - date of commit. For scripting purposes you can use UNIX timestamp - `%at`.

`%s` - commit message

How to format our commad to use these?

`git log --pretty` - this is how we start.

Please remember about `q` ;)

So let's try

`clear && git log --graph --pretty="%C(yellow) Hash: %h %C(blue)Date: %ad %C(red) Message: %s " --date=human`

Please, go through the command and understand all arguments.

Let's test some different ideas. Try to guess what the command output will be, before you execute them!

`clear && git log --graph --pretty="%ad" --date=short`

For better clarity you can add `format` to parameter

`git log --graph --pretty=format:"%ad" --date=short`

It will do the same. Here are another examples.

`clear && git log --graph --pretty="%ad"`

`clear && git log --graph --pretty="%at"`

`clear && git log --graph --pretty="%as"`

`clear && git log --graph --pretty="%C(bold blue)%h"`

`clear && git log --graph --pretty="%C(bold blue)%h %Cred%s %C(Yellow)by %an"`

Another example found on the Internet

`clear && git log --graph --pretty=format:"%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset" --abbrev-commit`

But... Will you enter this command every single time? No? What you need is on the next page :)