# *Git*ting comfortable

## Course theory

Read the [course material](https://mftenergy.github.io/git-course/1)

## Exercises

Pressing the link below opens a cloud shell in google with a cloned environment of the current repo containing the exercises.

[![Open in Cloud Shell](https://gstatic.com/cloudssh/images/open-btn.svg)](https://console.cloud.google.com/cloudshell/editor?cloudshell_git_repo=https://github.com/mftenergy/git-course.git)

<details>
  <summary>On your local machine</summary>
  
![Quick Start](/images/git_clone.gif)

- Clone this repository
- Go into the folder you want to solve an exercise in
- Run the `setup.sh` script
- Consult the README.md in that folder to get a description of the exercise

</details>

You start an exercise by pathing into the directory of the exercise and running `./setup.sh` (or `./setup.ps1` if you are on windows)

## Purpose

We want to introduce new employees to Git, as it as vital part of writing software. It ensure we create consistency, coherency and keep a well structured history that can be create collaboratively with other peers.

This repo is a collection of exercises that without a shame is stolen from [git katas](https://github.com/eficode-academy/git-katas).

The repo is serves a self-educational purpose, with a presentation that outlines the theory around the exercises.

Git katas has more exercises than the ones shown in here, so feel free to check them out if you want!

## Suggested Learning Path

0. [setup-git-client](setup-git/README.md) - Setup your git client in order to do git operations like `commit`
1. [basic-commits](basic-commits/README.md) - Very basic creation of commits.
2. [basic-staging](basic-staging/README.md) - Interacting with the stage (index).
3. [basic-branching](basic-branching/README.md) - The first stride into branching.
4. [rebase-branch](rebase-branch/README.md) - Using rebase as an alternative to merging.
5. [basic-revert](basic-revert/README.md) - Use revert to revert a change
6. [reset](reset/README.md) - Reset is a powerful and slightly dangerous command if you do not know what you are doing. Go through the three modes of resetting here.
7. [basic-stashing](basic-stashing/README.md) - The first stride into stashing.

See [Overview.md](Overview.md) for a more complete list and suggested order.

## Contributing

If you miss exercises or find errors in any of them, feel free to improve them and make a pull request.

You can also make an issue so we notice an opportunity to improve!

Thank you!

## Cheatsheet

A collection of useful commands to use throughout the exercises:

```shell
# Initializing an empty git repository.
git init            # Initialize an empty git repository under current directory.

# Cloning a repository
git clone https://github.com/praqma-training/gitting-comfortable.git      # Clone this repository to your current working directory

# Git (user and repo level) configurations
git config --local user.name "Repo-level Username"          # For setting a local git repo level user name.
git config --local user.email "Repo-level.Email@Example.com" # For setting a local git repo level user email.
                                                            # --global -> User level git config stored in <user-home>/.gitconfig for e.g. ~/.gitconfig
                                                            # --local -> repo level config stored in repo's main dir under .git/config


# See local changes
git status                  # Show the working tree status
git diff                    # Show changes current working directory (not yet staged)
git diff --cached           # Show changes currently staged for commit

# Add files to staging (before a commit)
git add myfile.txt          # Add myfile.txt to stage
git add .                   # Add entire working directory to stage

# Make a commit
git commit                              # Make a new commit with the changes in your staging area. This will open an editor for a commit message.
git commit -m "I love documentation"    # Make a new commit with a commit message from the command line
git commit -a                           # Make a new commit and automatically "add" changes from all known files
git commit -am "I still do!"            # A combination of the above
git commit --amend                      # Re-do the commit message of the previous commit (don't do this after pushing!)
                                        #   We _never_ change "public history"
git reset <file>                        # Unstage a staged file leaving in working directory without losing any changes.
git reset --soft [commit_hash]          # resets the current branch to <commit>. Does not touch the staging area or the working tree at all.
                                        # --hard mode would discard all changes.

# Configuring a different editor
## Avoid Vim but stay in terminal:
- `git config --global core.editor nano`

## For Windows:
- Use Notepad:
`git config --global core.editor notepad`

- or for instance Notepad++:
`git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"`


# See history
git log             # Show commit logs
git log --oneline   # Formats commits to a single line (shorthand for --pretty=oneline  --abbrev-commit )
git log --graph     # Show a graph commits and branches
git log --pretty=fuller     # To see commit log details with author and committer details, if any different.
git log --follow <file>     # List the history of a file beyond renames
git log branch2..branch1    # Show commits reachable from branch1 but not from branch2

# Deferring
git stash                               # Stash (store temporarily) changes in working branch and enable checkingout a new branch
git stash list                          # List stored stashes.
git stash apply <stash>                 # Apply given <stash>, or if none given the latest from stash list.


# Working with Branches
git branch my-branch       # Create a new branch called my-branch
git switch my-branch     # Switch to a different branch to work on it
git switch -c my-branch  # Create a new branch called my-branch AND switch to it
git branch -d my-branch    # Delete branch my-branch that has been merged with master
git branch -D my-branch    # Forcefully delete a branch my-branch that hasn't been merged to master

# Merging
git merge master         # Merge the master branch into your currently checked out branch.
git rebase master        # Rebase current branch on top of master branch

# Working with Remotes
git remote              # Show your current remotes
git remote -v           # Show your current remotes and their URLs
git push                # Publish your commits to the upstream master of your currently checked out branch
git push -u origin my-branch  # Push newly created branch to remote repo setting up to track remote branch from origin.
                              # No need to specify remote branch name, for e.g., when doing a 'git pull' on that branch.
git pull                # Pull changes from the remote to your currently checked out branch

# Re/moving files under version control
git rm <path/to/the/file>                 # remove file and stage the change to be committed.
git mv <source/file> <destination/file>   # move/rename file and stage the change to be committed.

# Aliases - it's possible to make aliases of frequently used commands
#   This is often done to make a command shorter, or to add default flags

# Adding a shorthand "sw" for "switch"
git config --global alias.sw "switch"
# Usage:
git sw master     # Does a "git switch master"

## Logging
git log --graph --oneline --all # Show a nice graph of the previous commits
## Adding an alias called "lol" (log oneline..) that shows the above
git config --global alias.lol "log --graph --oneline --all"
## Using the alias
git lol     # Does a "git log --graph --oneline --all"
```

## Testing

There is a very small test that you can run in powershell or bash.
It is contained in the scripts `test.sh` and `test.ps1`.

### Cleanup

You can remove testing artifacts, `exercise` directories, with the git clean command:

```sh
git clean -ffdX
```
