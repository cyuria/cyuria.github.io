# Gitting Gud

Every time I see someone teach git, they use confusing diagrams which just don't
help. At all.

Here's my take on git, without the stupid diagrams that make no sense.

## What is Git?

Git is a tool created by Linus Torvalds to manage different versions of the
linux kernel source code. It has since become the most used version control
system in the world.

The most core aspect of git is called a commit. A commit is a series of changes
to some code, which can be analogous to a videogame save file. Essentially, a
single commit stores a series of changes and a parent commit. The parent commit
is the previous commit made, thus through a chain of parent commits, you can
store every sequence of changes made to get to a specific version of code. Thus,
in a lot of situations, a git commit acts like a save file, which you can go
back to at any point in time.

You can create a git "repository" in a directory by running `git init`. More on
that later, including what a repository is. For now, just know you need to do it
before you can start working with git for a project.

The other useful command you might want is `git status`. This allows you to see
a lot of useful information about the current state of your local git
repository, including changes to the "working tree" (the stuff tracked by git).

One last thing is to read through git's output. It often contains useful
information and hints on what you might want to do.

### Creating a Commit

To create a commit, simply run `git commit` in the shell. You may wish to
specify a number of command line flags, such as `-m` which will let you specify
a message from the command line instead of being dropped into vim.

By default, git won't commit any changes when you run `git commit`. This is
because you need to specify which changes you want to commit. You do this with
the `git add` command. For example, to add every change in a file called
`README.md`, run `git add README.md`

At this point, I recommend you open up a terminal and make a few commits. These
will be useful for the rest of this tutorial.

Remember, if you're having trouble, don't hesitate to google things and consult
the git man pages.

### Time Travel

Let's say you want to go back in time to a previous commit. This is where the
`git reset` command comes in. You simply provide it with enough of the commit
hash to uniquely identify whatever commit you want to go back to and git will do
the rest.

But what is a commit hash and how do I get it? A commit hash is a series of
hexadecimal characters which can uniquely identify any commit ever created using
the magic of cryptography. You can find a commit hash via a couple different
ways, however the main one is `git log`. If you run `git log` it will open up
the `less` command with a history of everything. You can instead pipe git log
into other tools like `head` or use the `-n` flag to reduce the number of
commits shown.

Next to each commit will be a long string of seemingly random letters and
numbers. This string is your commit hash. Now go back and read this section
again.

Another useful tool for finding commits is `git bisect`. I suggest you do your
own research on this as I will not explain it here. Bisecting can be useful if
you don't know which commit broke something and you want to find said commit.

### Undoing Stuff

Using `git reset` won't always be helpful, as there are certain issues with time
travel. Those mainly being that it's rather hard to communicate back and forth
with someone in a different timeline. That's where `git revert` comes in. Git
revert allows you to undo the changes in one commit with another commit. This
ensures time only travels forwards. It's like building a house and then
demolishing it instead of travelling back it time to before it was built. This
ensures everyone stays on the same timeline.

You may also want to use `git revert` if you have a few commits in between the
one you are undoing and the current git head (a shorthand for the latest
commit).

Sometimes you will also end up with a situation where `git log` isn't enough.
I'd encourage you to also look at `git reflog` for these niche situations.

### Branches

Before we can properly introduce remotes (i.e. cloud storage for git), we first
need the concept of branches.

Going back to our analogies of timelines and videogame saves, a branch is like
going back in time to some previous save and continuing development in a
different path, thus creating effectively a new timeline with it's own unique
set of saves.

Git has this idea of "merging" two branches, which means changing the state of
any tracked files (i.e. the worlds of the two timelines you you are combining)
so that they become the same.

Let's say in one timeline someone builds a house with a pool and a shed and in
another timeline someone builds a mansion in that same spot. Merging would be
the process of finding some common point between the house and the mansion. This
could be just getting rid of the mansion and building an identical house and
pool, or it could be to remove the shed and build a wing, doing the equivalent
to the mansion to end up with a smaller mansion that also has a pool.

One thing to note about git is that in a new git repository created on the
command line, the default branch is named "master". This can of course be
configured, and due to various reasons many people use an alternative such as
"main" or "trunk" instead. A number of online git providers such as github and
gitlab also use one of these alternative names. There is nothing wrong with any
of these options (despite what some people online might tell you), but you
should be aware that this discrepancy does exist.

#### Git Commands

The git commands related to dealing with branches are as follows:
- `git checkout`
- `git branch`
- `git merge`
There are also a couple of other commands that I won't cover, those being
`git rebase` and `git cherry-pick`. I encourage you to research these on your
own, as they are both very useful tools.

The checkout subcommand allows you to switch branches. As a byproduct, it can
also be used to create a new branch from the current commit and switch to it.

The branch subcommand allows you to list, create and delete branches. You can
list branches with the `--list` option. Listing is also the default option, so
you can list branches with just `git branch`. Creating can be done with the `-c`
and `-C` flags and deleting with the `-d` and `-D` flags. Have a read through
the man pages if you want to learn more.

The merge subcommand allows you to merge changes from one branch into the
current branch. You may have to deal with merge conflicts, which occur when git
cannot automatically deal with the changes, such as if the same piece of code
has been altered differently, such as in the mansion and house analogy above.

If, continuing with the analogy, a public park was built in one timeline and a
house was built in another, git may be able to automatically merge these changes
if the public park and the house weren't built in the same place.

It is at this point that I suggest you go back to your command line and tinker
around with your previous commits. Try adding a new branch. Try merging it with
another one. Try inducing a merge conflict and dealing with that. Once you feel
you are familiar with this process, come back and continue on to the next
section.

Keep in mind that the git man pages and google are your friend. If something
hasn't clicked, have another read over it here. If it still doesn't make sense,
ask google or read through the relevant sections in the git man pages.

## Multiplayer

One of the great advantages of the way git is architected is that it allows for
people to collaborate on work without any kind of real time synchronisation,
which can be annoying if someone doesn't have internet, a pain if someone is
using a text editor which doesn't support it and expensive if someone has a slow
computer.

### Remotes

Git has a concept of remotes. Remotes are branches that aren't stored locally.
They can be stored somewhere else on your computer if you have the same
"repository" twice (keeping in mind that a git repository is an instance of a
codebase tracked by git), or somewhere on your network or the internet. Really
anywhere that can store files can also store a remote git repository.

I also won't continue with the analogies, because remotes are another layer on
top of the core git functionality and so the analogies won't help. If you are
still struggling to understand something, it may be because some of the previous
parts of this document don't make sense. Have another read over it and maybe try
google or the git man pages (see `man git`). It is also possible this tutorial
is simply not for you and you would be better off with another one. I strongly
encourage you to try things and use every resource you have available to you.

An "upstream" repository is a repository whose primary purpose is to serve as a
hub for changes, which will then trickle down to every other repository. This
means any changes "upstream" will eventually be reflected "downstream" on your
local machine. 

I won't go over setting up a remote, as most of the time you will be cloning a
git repository with `git clone`, which will automatically set the cloned url as
an upstream repository, however, as usual, google is your friend, as are the git
man pages.

There is usually only one remote, and it is usually called "origin", but this
may not always be the case.

### Syncing

The important thing to know about remotes is that they have their own set of
branches. These branches are kept in sync with `git pull` and `git push`. There
is also a `git fetch` command, but I won't go over it here.

The `git pull` command will download any changes on the remote repository and
pull them into the current branch. This may require dealing with merge
conflicts. There are a few useful options, including enabling `pull.rebase` with
`git config` or running `git pull --rebase` to avoid dealing with many merge
issues. I won't go into these here, however I suggest you do your own research
on the `git rebase` subcommand.

The `git push` command will upload any changes in the local repository to the
remote one. It is important to note that this only affects commits and not the
"working tree". The working tree is the current state of code in the repository,
regardless of if it has been committed or not, hence the term "working". The
"tree" part refers to the tree-like structure of directories.

There is one thing I haven't mentioned. Each repository has a number of
branches. Git doesn't know how to correlate these branches together, as they
could have different remote repositories they need to connect to. In order to
tell git which branches should go where, `git push` and `git pull` take some
extra arguments. The first one is the name of the remote or the remote branch to
push to. The second is the local branch to push changes from. Hopefully the
following examples will clear things up a bit.
```sh
git push origin master
git pull origin master
```

To make life easier, git can store upstream remotes for a branch. This can
either be done with `git branch` or while pushing with the `--set-upstream` flag
as follows:
```sh
# When creating a branch
git branch -c my-branch --track=inherit

# Leaving out my-branch will use the current branch
git branch --set-upstream-to=origin my-branch
git branch -u origin my-branch

# While pushing
git push --set-upstream origin master
git push -u origin master
```

Keeping in mind that the `-u` option is just shorthand for the relevant longer
form option.

Once this has been done, future pushes and pulls will use the previously set
upstream and you can simply use `git push`.

I strongly encourage you to set up a remote, either locally on using a website
such as [github](https://github.com/) or [gitlab](https://gitlab.com). There
are a number of good tutorials online on how to use these websites. The git man
pages for `git` and `git clone` have good information on the different ways to
clone a repository, including locally.

Now start playing around and seeing whats possible. Please don't do this on an
actual project until you are comfortable with git, as you may end up in a state
you don't know out to get out of.

### Forking

The last thing to mention about working with remote repositories is the idea of
"forks". Forks are a dedicated branch, which usually serves as an upstream for
developers, however are typically downstream of the original project. Typically
forks are merged back into the upstream repository at some point using what is
known as a "pull request".

The primary purpose of forks is to enable a developer to work on their own
remote copy of a project, with all the benefits of having said remote, without
allowing them direct write access to the original project's source code. Their
changes are then discussed and reviewed in a pull request, which may be merged
back into the original project. This enables a developer to create a feature or
fix a bug in their own fork, before sending the changes back upstream to the
original project.

There are also hard forks, which are effectively just a copy of the codebase and
are not considered to be downstream of the original project. Hard forks are not
intended to be merged into the original project and are instead used for
creating a new project based on the original.

## Missing Stuff

This tutorial is missing a few crucial aspects of git which I have left out
intentionally.

The first is working with git cloud providers[^1]. This is left out because this
tutorial is about git, not a specific git infrastructure provider.

The second thing is configuring git. There are a lot of options you can
configure with git using the `git config` subcommand. I haven't covered these
because I believe they are up to the individual git user and are subjective.
These config options allow you to change the look and feel of git as well as the
default behaviour of commands like `git status` and `git pull`. There are a lot
of options and I'd recommend going through the man pages for a list.

I've also not covered `git diff`. This is a very useful command which allows you
to view the changes made by one or more commits and/or the working tree.

Lastly, I haven't covered editor integrations. This is because git is text
editor agnostic, and therefore this tutorial should be too. For anyone who uses
vim or a derivative thereof, I can strongly suggest tpope's fugitive vim plugin
for working with git inside the editor.

## Extra Learning

There are a few commands which are very useful but I haven't properly covered
here. If you want to learn more on your own, here's a list:
- `git bisect`
- `git reflog`
- `git rebase`
- `git cherry-pick`
- `git fetch`
- `git diff`

## Copyright

Copyright (c) 2024-2025 Cyuria. All Rights Reserved.
