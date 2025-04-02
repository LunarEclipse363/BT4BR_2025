# Introduction
| Key |   Value    |
|====:|:===========|
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

### Staging files
| Command                       | Action                                          |
|===============================|=================================================|
| git add \[FILE...\]           | stages some file(s)                             |
| git reset \[FILE...\]         | unstages some file(s)                           |
| git restore \[FILE...\]       | discards changes made to the specified file(s)  |

### Commiting files
| Command                       | Flag        | Action                                       |
|===============================|=============|==============================================|
| git commit                    |             | creates a new commit                         |
| git commit                    | -a          | commits all modified files tracked by git    |
| git commit                    | -m \[MSG\]  | uses the specified message for the commit    |

### Managing remotes
TODO

### Pushing, pulling, fetching
TODO

### Manipulating commits
**Note:** You SHOULD NOT ever edit commits which you have already pushed, unless you're working on a branch.

| Command                       | Flag               | Action                                                                              |
|===============================|====================|=====================================================================================|
| git rebase -i HEAD~X          |                    | interactive rebase - edit X commits back                                            |
| git push                      | --force-with-lease | overwrite a remote branch (but only if it has not changed since we last fetched it) |

TODO: add more

### When you do an oopsie and a commit is gone
| Command                       | Flag        | Action                                                    |
|===============================|=============|===========================================================|
| git help reflog               |             | read the manual for the reflog subcommand                 |
| git reflog                    |             | show any recent commits even if they aren't on any branch |
