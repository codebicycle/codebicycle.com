# Git

[Git Reference][gitref] — learn the most commonly used Git commands.

[gitref]: http://git.github.io/git-reference/

***

> Rebasing is like saying, “I want to base my changes on what everybody has already done.”


    git checkout a6ba3a1 README.md

Log current branch

    git log --oneline

Log all branches

    git log --oneline --all --decorate --graph

Undo all fetches from remote A simply by removing this remote:

    git remote remove A

    git remote add A <path/to/repository>
    git fetch A <name of branch>

Delete local branch

    git branch -d feature/login

Delete remote branch

    git push origin --delete feature/login

Remove any local remote-tracking branches which no longer exist on the remote

    git fetch --prune

## Stash

    git stash

Apply the stash and then immediately drop it from your stack.

    git stash pop

## Push
    git push <where> <what>
    git push origin master

## Fetch Merge

    git fetch origin branch
    git merge --ff-only origin/deploy

## Diff

Differences between last known state and current state.

Diff between staging area and working directory

    git diff
    git difftool

Diff between last commit on the current branch and working directory

    git diff HEAD
    git difftool HEAD

Diff between last commit on the current branch and staging area

    git diff --staged HEAD

Diff between a given commit and the latest one

    git diff a6ba3a1 HEAD
    git diff HEAD~3 HEAD

Diff between branches

    git diff master origin/master

Limit to one file

    git diff -- README.md


## Resources

- Git Essentials LiveLessons
