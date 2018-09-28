<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
# puns
A git repository to practice submitting Pull Requests (PRs) to open source project. Also, a collection of puns.

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
If there are alternate ways to doing these operations or if you have references you would like to share. Submit a PR!

## Code of Conduct
No judgement! Treat everyone like human beings who deserve respect. We were all noobs once.

## How to configure your git
Before you do anything, set up your gitconfig!

```
$ git config --global user.name="Pun Princess"
$ git config --global user.email=punprincess@punworld.net
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

Note: all the links below can be copied from the GitHub page of the repo using the top right green button that says `Clone or download`. Make sure it says `Clone with SSH`. If you haven't set up your SSH Keypair using the instructions above, you can still use `Close with HTTPS`. You'll end up entering your username and password a lot though.

The original project which you have forked from is called `upstream`.

```
$ git clone <your clone>
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

## How to update your GitHub fork to get new changes from the original project

Assuming you have no new local changes

```
$ git pull --rebase
```

## How to update your commit
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
