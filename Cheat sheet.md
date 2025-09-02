# Creating a repository

`git init`

`git clone`

`git clean` : Remove untracked files in your working repository.
- `-d` : Include untracked directories
- `-x` : Include ignored files (files in .gitignore)
- `-n` or `--dry-run` : See what it will delete
- `f` or `--force` : Necessery to have this option because it will permanently delete files

# Info about your repository

`git log`
- `--all` : All branches, not only the current one. 
- `--oneline` : Only the commit hash and the commit message will appear
- `--graph` : Usefull to see merge

`git show`

`git status`

`git blame`

# Commiting

`git add`
- `-p` or `--patch` : Allow you to stage part of a file
- `-i` : Interactive add

`git rm`

`git mv`

`git commit`
- `-m` or `--message` : Include the message (if omited, the editor will open)
- `-a` or `--all` : Include all change (skip staging), modified or deleted but not new files
- `--ammend` : Modify the last commit

# Branching

`git branch <branchName>`
- `-d` or `--delete` : Delete a branch
- `-f` `--force <branchName> <commit>` : Move the branch to another commit

`git switch <branch>`
- `-c` or `--create` : Create and switch branch
- `-d` or `--detached` : Used for detached HEAD, like switching to a remote branch
- `-` : Shortcut to switch to the previous branch.

`git merge <branch>` : Pull the branch toward you
- Allow you to fast foward

`git rebase <branch>` : Push you toward the branch
- `git rebase <mainBranch> <featureBranch>` : If you want to rebase 2 branches without having to `git switch` to *mainBranch* first

# Others

`git cherry-pick`

`git tag`

# Reverting change

`git restore [--] <pathspec>`
- `--source`
- `--staged`
- `--worktree`

`git revert`

`git reset`
- `--soft` : Update just the branch 
- `--mixed` : Update the branch then the index
- `--hard` : Update the branch, the index, and then the working directory
- `-p` or `--patch` : Partially reseting a file

# Stash

`git stash [push] [<pathspec>]` : Add all your modified files to a temporary stash
- `-m` or `--message` : Add a message to remember what you were doing.
- `-u` or `--include-untracked ` : Keep new files that you add without having `git add` them yet
- `-S` or `--staged` : Stash only what is in your staging area (index)

`git stash pop` : Restore all your modified files

`git stash list` : List all your stash

`git stash show` : Show the diff of a stash

`git stash clear` : Delete all stash

`git stash drop [stash]` : Delete a specifi stash (from `git stash list`)

# Remote

`git fetch`

`git pull`

`git push`

# Debuging

`git bisect`

`git diff`
