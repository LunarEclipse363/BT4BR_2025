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

### Getting help
| Command                       | Flag           | Action                                                         |
|-------------------------------|----------------|----------------------------------------------------------------|
| git help \<SUBCOMMAND\>       |                | prints help for a given git subcommand                         |
| git \[SUBCOMMAND\]            | --help         | prints help for the command/subcommand                         |
| man \<CMD\>                   |                | shows the manual for (almost) any linux shell command          |
| apropos \<QUERY\>             |                | shows all shell commands containing QUERY in their description |
| whatis \<CMD\>                |                | shows a summary of what a command does                         |

### Initializing a repository
| Command                       | Flag           | Action                                                   |
|-------------------------------|----------------|----------------------------------------------------------|
| git init                      |                | creates an empty repository in the current directory     |
| git remote add origin \<URI\> |                | adds a remote named `origin` with the specified URI      |
| git push \<BRANCH\>           | -u \<REMOTE\>  | pushes BRANCH to REMOTE and sets it as the branch origin |

### Staging files
| Command                       | Flag        | Action                                           |
|-------------------------------|-------------|--------------------------------------------------|
| git add \<FILE...\>           |             | stages some file(s)                              |
| git add                       | -i          | stages specific changes in some files you select |
| git reset \<FILE...\>         |             | unstages some file(s)                            |
| git restore \<FILE...\>       |             | discards changes made to the specified file(s)   |
| git mv \<SRC\> \<DST\>        |             | moves SRC to DST and tells git that about it     |
| git rm \<FILE\>               |             | deletes the FILE and tells git about it          |

### Commiting files
| Command                       | Flag        | Action                                       |
|-------------------------------|-------------|----------------------------------------------|
| git commit                    |             | creates a new commit                         |
| git commit                    | -a          | commits all modified files tracked by git    |
| git commit                    | -m \<MSG\>  | uses the specified message for the commit    |

### Viewing commits
> **Note:** the `HEAD` ref points to what you have checked out.  
> You can reference previous commits with `HEAD~X` where X is a number.  

| Command                       | Flag           | Action                                                   |
|-------------------------------|----------------|----------------------------------------------------------|
| git diff \<REF1\> \<REF2\>    |                | show the changes between REF1 and REF2                   |
| git diff \<REF1\> \<REF2\>    | --unified      | nicer format                                             |
| git diff \<REF1\> \<REF2\>    | --color        | colors the output                                        |
| git log                       |                | shows a list of commits on the current branch            |
| git log                       | --all          | shows a list of commits on all branches                  |
| git log                       | --graph        | draws a graph of branches to the left of the commits     |

### Managing remotes
| Command                                        | Action                                                   |
|------------------------------------------------|----------------------------------------------------------|
| git remote                                     | lists available remotes                                  |
| git remote rename \<OLD\> \<NEW\>              | renames OLD remote to NEW                                |
| git remote remove \<NAME\>                     | delete the remote called NAME                            |
| git remote get-url \<NAME\>                    | print the url of the remote NAME                         |
| git remote set-url \<NAME\> \<NEWURL\>         | change the URL of the remote NAME to NEWURL              |

### Pushing, pulling, fetching
| Command                       | Flag           | Action                                                   |
|-------------------------------|----------------|----------------------------------------------------------|
| git fetch                     | --all          | fetch the changes from all known remotes                 |
| git pull                      |                | fetch and apply any updates to the current branch        |
| git push                      |                | push the local changes to a remote                       |

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
> **Note:** You SHOULD NOT ever edit commits which you have already pushed (<abbr title="also known as">AKA</abbr> overwrite history).  
> Except when you're working on a branch where you can force-push.  
> Force-pushing is typically forbidden for the default (main) branch.  

To get more precise information about how these work see `git help <GIT_SUBCOMMAND>`.

The `git rebase` command is useful for resolving conflicts with a remote version of a branch - you can simply rebase on the remote branch to move your local changes on top of whatever other changes were added in the meantime.
A typical workflow in that case would be `git fetch`, then `git rebase`, then `git push`.

| Command                       | Flag               | Action                                                                              |
|-------------------------------|--------------------|-------------------------------------------------------------------------------------|
| git rebase -i HEAD~X          |                    | interactive rebase - edit X commits back                                            |
| git rebase \<UPSTREAM\>       |                    | reapply the commits on the current branch on top of a different branch, and save    |
| git push                      | --force-with-lease | overwrite a remote branch (but only if it has not changed since we last fetched it) |
| git revert \<COMMIT\>         |                    | creates a new commit that reverts the changes from the specified COMMIT             |
| git cherry-pick \<COMMIT\>    |                    | picks a specific COMMIT from another branch and adds it to the current one          |
| git merge \<BRANCH\>          |                    | merges changes from another branch into the current one (see `git help merge`)      |

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

