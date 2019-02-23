<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
# puns
A git repository to practice submitting Pull Requests (PRs) to an open source project. Also, a collection of puns.

## What it's about

- You want to contribute to an open source project but you don't know how.
- You have submitted a PR to an open source project but you are asked to update your PR and you don't know how.
- You have submitted a PR to an open source project but you now have to resolve conflicts and you don't know how.

This project is meant to be
- A tutorial on how to maintain your fork of an open source project hosted on GitHub.
- A no-commitment, no-judgement, make-all-the-mistakes-you-want, practice open source project.

## File issues against this project
If you feel there is a problem you have run into that isn't covered in the tutorials below, please create an issue with a detailed description on the situation where you were trying to submit a PR. I will try my best to either point you to the instructions that should help or enter a list of commands you should be using.

## Practice PRs to this project
Let me know what operation you want to practice and I will set it up for you. Operations include dealing with conflicts, rebase, merge or updating a PR.

## Real PRs to this project
If there are alternate ways to doing these operations or if you have references you would like to share, please submit a PR!

## Code of Conduct
No judgement! Treat everyone like human beings who deserve respect. We were all n00bs once.

## How to configure your git
Before you do anything, set up your gitconfig!

```
$ git config --global user.name "Pun Princess"
$ git config --global user.email punprincess@punworld.net
```

## How to not enter your username and password everytime you interact with GitHub from the command line
Create an SSH Keypair and add the public key to your GitHub account

```
$ ssh-keygen
```
Enter a passcode for your keypair. Once done:
```
$ cat ~/.ssh/id_rsa.pub
```
Copy the output. Go to your profile picture on the top right corner of your GitHub account, click on `Settings`. On the left hand side, click on `SSH and GPG keys`. Click the green button that says `New SSH key`. Enter a Title. Then paste the output above into the text box under Key. Click on the green button that says `Add SSH key`.

## How to submit PRs with your GitHub fork

You have forked the Open Source project you want to contribute to on GitHub. Now what?

Note: all the links below can be copied from the GitHub page of the repo using the top right green button that says `Clone or download`. Make sure it says `Clone with SSH`. If you haven't set up your SSH Keypair using the instructions above, you can still use `Clone with HTTPS`. You'll end up entering your username and password a lot though.

The original project which you have forked from is called `upstream`.

```
$ git clone <your clone>
$ cd puns
$ git remote add upstream git@github.com:nishakm/puns.git
$ git fetch upstream
$ git checkout -b work-to-submit upstream/master
```

Once you've completed your work, it's time to commit your changes.

```
$ git add <files>
$ git commit -s
```

Good commit messages are usually formatted in this way:

```
Title of the commit; Limit to 50 characters

Body of the commit
Explain what the change does and why
Limit to 70 characters per line

Resolves/Fixes #<github issue number if there is one>

Signed-off-by: Pun Princess <punprincess@punworld.net>
```

After committing, upload your changes to your fork of the repo.

```
$ git push origin work-to-submit
```

You should get a link to the page to submit your PR to the original project.

Here is a demo:
[![asciicast-setuprepo](https://asciinema.org/a/203606.png)](https://asciinema.org/a/203606)

## How to update your GitHub fork to get new changes from the original project

Assuming you have no new local changes: when you run `git status` you should not see files modified or staged for commit.

```
$ git pull --rebase
```

But what if you do have files that are modified? Use the `git stash` to save your changes.

```
$ git stash push
$ git pull --rebase
$ git stash pop
```

## How to update your commit with changes to files
The maintainer of the original project asks you to make some changes to your PR. You've gone ahead and made the changes to the files. Now:

```
$ git add <files>
$ git commit --amend
```

Make changes to the commit message if you need to.

```
$ git push -f origin work-to-submit
```

Your PR will be automatically updated.

*HOLD UP!* Did someone tell you `-f` or force push was bad? Forced updates on your own fork when nobody else is working on it is fine. If you mess up you can still pull changes from upstream and start fresh. But remember, *never* `git push -f upstream`!

## How to add a Signed-off-by to your commit message
A Developer Certificate of Origin (DCO) is required in your commit message. If you have set up your gitconfig, this is easy. Do:

```
$ git commit --amend -s
```

Check your commit message. Once saved:

```
$ git push -f origin work-to-submit
```

Your PR will be automatically updated.

## How to resolve conflicts in your PR
You notice that the PR that you have submitted wants you to resolve conflicts. If you have followed the above setup, here's what you do:

```
$ git pull --rebase <-- this will say you have conflicts to resolve
$ git status <-- this will tell you what files have conflicts
```

Edit the files to resolve the conflicts. Once ready:

```
$ git add <files>
$ git rebase --continue
$ git commit --amend
```

Make sure your commit message is OK.

```
$ git push -f origin work-to-submit
```

Your PR will be automatically updated.

You can watch a demo here:
[![asciicast-resolveconflicts](https://asciinema.org/a/203608.png)](https://asciinema.org/a/203608)

## How to combine two or more commits into one (squash)
Sometimes, the maintainer will ask you to change something in your commit, and you may instead add another commit to your PR (maybe you didn't know about force pushes). The maintainer may then ask you to squash your commits, that means combining your commits into one big commit (we won't go into reasons why a maintainer may as you to do this - there are several reasons why). This is where `git rebase -i` helps:

```
$ git rebase -i HEAD~<count from HEAD to the first commit on your PR branch>
```

For example, you submitted 3 commits in your PR. To squash all 3 you can run:

```
$ git rebase -i HEAD~3
```

Running this will open up your default editor. It will show something like this:

```
pick 4e9a282 Added bark pun to dogs <-- first commit
pick ae74d75 Added sniffing pun to dogs <-- second commit
pick 3344294 Added howl pun to dogs <-- third commit

# Rebase eb0ef4c..3344294 onto eb0ef4c (3 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified). Use -c <commit> to reword the commit message.
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

To combine all 3 together, change the second and third commit to `squash`. Then save the file via your text editor.

```
pick 4e9a282 Added bark pun to dogs
squash ae74d75 Added sniffing pun to dogs
squash 3344294 Added howl pun to dogs
```
   
You should get something like this:

```
# This is a combination of 3 commits.
# This is the 1st commit message:

Added bark pun to dogs

Signed-off-by: Nisha K <nishak@vmware.com>

# This is the commit message #2:

Added sniffing pun to dogs

Signed-off-by: Nisha K <nishak@vmware.com>

# This is the commit message #3:

Added howl pun to dogs

Signed-off-by: Nisha K <nishak@vmware.com>

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
```

As the message says - anything with `#` at the beginning will be ignored. So imagine your commit message looking like this:

```
Added bark pun to dogs

Signed-off-by: Nisha K <nishak@vmware.com>

Added sniffing pun to dogs

Signed-off-by: Nisha K <nishak@vmware.com>

Added howl pun to dogs

Signed-off-by: Nisha K <nishak@vmware.com>
```

You probably want to make this more readable. After editing, save using your text editor. Now you can resubmit your PR:

```
$ git push -f origin work-to-submit
```

## How to make your master catch up with upstream's master
You may have noticed that we have been working on top of the upstream's branches and not your fork's copy of the upstream's branches. So after a while, you would probably want your fork to match upstream. This is an operation that uses git's [`plumbing` rather than `porcelain`](https://git-scm.com/book/en/v2/Git-Internals-Plumbing-and-Porcelain).

```
$ git checkout -b up upstream/master
Branch 'up' set up to track remote branch 'master' from 'upstream'.
Switched to a new branch 'up'
$ git push origin up:refs/heads/master
```

Why not `git push origin master`? Well, `master` is pointing to the tip of the fork's master branch which is already up to date with the remote's `master`, so there isn't anything for git to do. `git push origin up:refs/heads/master` pushes your local copy of upstream/master to the remote `origin` to a specific branch reference called `refs/heads/master` which is your remote's actual master branch.

Now to update your local master branch:
```
$ git checkout master
$ git pull
```

If you have never worked on this branch, the pull should succeed. You can do this for any upstream branch.
