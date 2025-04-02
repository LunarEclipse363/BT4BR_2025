# Introduction
| Key |   Value    |
|----:|:-----------|
|Name |    Luna    |
|Date | 2025-04-02 |

## Git commands cheatsheet
### Initial Setup
Setting up user information:

```fish
git config --global user.name "LunarEclipse"
git config --global user.email "luna@lunareclipse.zone"
```

Generating an SSH key:
```fish
ssh-keygen -t ed25519 -C "$(whoami)"@"$(hostname)"
```

Changing password for SSH key:
```fish
ssh-keygen -p -f $private_key_filename
```

Printing the public key for a private key (if you lose the .pub file):
```fish
ssh-keygen -e -f $private_key_filename
```

### Initializing a repository
| Command                       | Flag           | Action                                                   |
|-------------------------------|----------------|----------------------------------------------------------|
| git init                      |                | creates an empty repository in the current directory     |
| git remote add origin \<URI\> |                | adds a remote named `origin` with the specified URI      |
| git push \<BRANCH\>           | -u \<REMOTE\>  | pushes BRANCH to REMOTE and sets it as the branch origin |


### Staging files
| Command                       | Action                                          |
|-------------------------------|-------------------------------------------------|
| git add \<FILE...\>           | stages some file(s)                             |
| git reset \<FILE...\>         | unstages some file(s)                           |
| git restore \<FILE...\>       | discards changes made to the specified file(s)  |
TODO: git mv
TODO: git rm

### Commiting files
| Command                       | Flag        | Action                                       |
|-------------------------------|-------------|----------------------------------------------|
| git commit                    |             | creates a new commit                         |
| git commit                    | -a          | commits all modified files tracked by git    |
| git commit                    | -m \<MSG\>  | uses the specified message for the commit    |

### Viewing commits
| Command                       | Flag           | Action                                                   |
|-------------------------------|----------------|----------------------------------------------------------|
TODO: git diff
TODO: git log

### Managing remotes
| Command                       | Flag           | Action                                                   |
|-------------------------------|----------------|----------------------------------------------------------|
TODO: git remote

### Pushing, pulling, fetching
| Command                       | Flag           | Action                                                   |
|-------------------------------|----------------|----------------------------------------------------------|
TODO: git fetch
TODO: git pull
TODO: git push

### Branches
| Command                       | Flag           | Action                                                   |
|-------------------------------|----------------|----------------------------------------------------------|
| git checkout                  | -b \<NAME\>    | creates a new branch called NAME and switches to it      |
| git branch                    |                | lists local branches                                     |
| git branch                    | --all          | lists all branches                                       |
| git branch                    | -d \<BRANCH\>  | deletes the branch BRANCH                                |

### Tags
Tags are human-readable names we can assign to a specific version (commit).

Usually immutable (never change), and used for tagging released versions of a software (i.e. `v1.2.3`).


| Command                       | Flag           | Action                                                   |
|-------------------------------|----------------|----------------------------------------------------------|
| git tag                       |                | shows a list of all tags                                 |
| git tag \<NAME\> \[COMMIT\]   |                | creates a tag named NAME on the current commit or COMMIT |
| git tag \<NAME\> \[COMMIT\]   | -m \<MESSAGE\> | adds a message to the tag instead of asking you for one  |
| git push                      | --tags         | pushes all tags to the default remote                    |


### Stash
The stash lets you save any staged files into a temporary place while you work on something else.

| Command                       | Flag           | Action                                                           |
|-------------------------------|----------------|------------------------------------------------------------------|
| git stash                     |                | pushes the currently staged files to a new unnamed stash         |
| git stash \[push\]            | -m \<MESSAGE\> | like above but gives the stash a description                     |
| git stash pop                 |                | removes the most recent stash and applies it to the working tree |
| git stash list                |                | shows the stash stack                                            |
| git stash drop \[STASH\]      |                | removes the specified STASH without applying it                  |

See `git help stash` for more information.

### Manipulating commits
**Note:** You SHOULD NOT ever edit commits which you have already pushed (<abbr title="also known as">AKA</abbr> overwrite history), unless you're working on a branch where you can force-push (typically forbidden for the default branch, which is usually `main`).

| Command                       | Flag               | Action                                                                              |
|-------------------------------|--------------------|-------------------------------------------------------------------------------------|
| git rebase -i HEAD~X          |                    | interactive rebase - edit X commits back                                            |
| git push                      | --force-with-lease | overwrite a remote branch (but only if it has not changed since we last fetched it) |
TODO: git revert
TODO: git cherry-pick
TODO: git merge
TODO: git rebase| | useful for resolving common conflicts, fetch -> rebase -> push

### When you do an oopsie and a commit is gone
Git actually keeps commits that aren't bound to any branch/tag for a while before garbage-collecting them, so usually if you quickly realize your mistake you will be able to recover from it.

The main command here is `git reflog`, it will show you a list of all commits you've recently checked out, so you can copy the commit ID you lost and get it back.

| Command                       | Flag        | Action                                                                                   |
|-------------------------------|-------------|------------------------------------------------------------------------------------------|
| git help reflog               |             | read the manual for the reflog subcommand                                                |
| git reflog                    |             | show any recent commits even if they aren't on any branch                                |
| git checkout \<REF\>          |             | switches your working tree to REF, use `git checkout -b <NAME>` to create a branch on it |
| git reset \<REF\>             |             | resets the current branch to REF (i.e. commit id), doesn't modify your working tree      |
| git reset \<REF\>             | --hard      | resets the branch like above, but also **OVERWRITES** files in the working tree          |
