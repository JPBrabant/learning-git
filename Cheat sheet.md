# Help

`git help <command>`

# Creating a repository

`git init`

`git clone`

`git clean` : Remove untracked files in your working repository.
- `-d` : Include untracked directories
- `-x` : Include ignored files (files in .gitignore)
- `-n` or `--dry-run` : See what it will delete
- `-f` or `--force` : Necessery to have this option because it will permanently delete files

# Info about your repository

`git log`
- `--all` : All branches, not only the current one. 
- `--oneline` : Only the commit hash and the commit message will appear
- `--graph` : Usefull to see merge
- `--follow <path>` : See all commit that change a file.

`show`
- `git show <commit>:<path>` : Show the content of a file at a specific `<commit>`, if `<commit>` is omited, the index is assumed

`git status`

`git blame`

`git grep`

`git diff`
- `--name-only`
- `--cached|--staged`

`ls-files`
- `git ls-files`      : Show the list of file 
    - `(-c|--cached)` : Show all files cached in Git’s index, i.e. all tracked files
    - `(-s|--stage)`  : Show staged contents


# Commiting

`add`
-`git add`
    - `(-p|--patch)` : Allow you to stage part of a file
    - `(-A|-all)`    : All files in the entire working tree are updated in the index

`rm`
- `git rm <file>`          : Removes the file from the index and deletes it from the working directory (next commit shows the file deleted, tell git to stop tracking the file)
- `git rm --cached <file>` : Removes the file from the index but keep it on disk as an untracked file

`git mv`

`git commit`
Git creates a new commit and moves the branch that HEAD points to, up to it.
- `-m` or `--message` : Include the message (if omited, the editor will open)
- `-a` or `--all` : Include all change (skip staging), modified or deleted but not new files
- `--ammend` : Modify the last commit

# Branching

`branch`
- `git branch`                                          : List all local branches
    - `(-a|--all)`                                      : List all local and remote branches
- `git branch <branch-name>`                            : Create a branch (but don't switch to it)
    - `<start-point>`                                   : By default, `start-point` is `HEAD` but it can be a tag, commit hash, ancestry, HEAD or branch name
- `git branch (-m|--move) <old-name> <new-name>`        : Rename
- `git branch (-d|--delete) <branch-name>`              : Delete
- `git branch (-f|--force) <branch-name> <start-point>` : Move the branch to a new commit

`switch`
This command change where HEAD is pointing and try to update both the working directory and the index with the content of the commit. If you have uncomited change that would conflit, the command abort. 
- `git switch <branch>`                      : Move HEAD to a branch (`-` shortcut for the previous branch)
    - `(-c|--create)`                        : Create and switch branch
- `git switch (-d|--detached) <start-point>` : Used for detached HEAD (switch to a specific commit or a remote branch because you can't edit a remote branch)

`merge`
- `git merge <commit>`             : Incorporates changes from the named commits (since the time their histories diverged) into the current branch
    - *Fast-foward*                : If the current branch is an ancestor of `<commit>`, current branch will simply move
- `git merge (--continue|--abort)` : Fix merge conflict and then continue (you need to tell git that the conflict has been resolved with `git add`) or abort

`rebase`
- `git rebase <destination-branch>` : Move changes from the current branch (since the time their histories diverged) to `<destination-branch>`
    - `<source-branch>`             : Move changes from `<source-branch>` to `<destination-branch>`
    - `(-i|--interactive)`          : Manual rebase allow you to rewrite history (reorder, rewrite message, split or squash, ...)
    - *Fast-foward*                 : If the current branch is an ancestor of `<destination-branch>`, current branch will simply move
- `git rebase (--continue|--abort)` : Fix merge conflict and then continue (you need to tell git that the conflict has been resolved with `git add`) or abort
- `git rebase --onto <newbase> <upstream> <branch>` : Take everything between `<upstream>` and `<branch>` and put it on `<newbase>`

`git cherry-pick`

# Reverting change

`restore`
Staged and worktree can both be used, if none is used, workstree is assumed. If source is omited, for staged, HEAD is assumed, for worktree, the index is assumed.
- `git restore --source <commit> <file>`
    - `--staged`   : Restore `<file>` from `<source-commit>` to the staging area
    - `--worktree` : Restore `<file>` from `<source-commit>` to the working directory
- `git restore <file>`                              : Restore working directory `<file>` from the index
- `git restore --worktree <file>`                   : Restore working directory `<file>` from the index
- `git restore --staged <file>`                     : Restore index `<file>` from HEAD
- `git restore --staged --worktree <file>`          : Restore index and working directory `<file>` from HEAD
- `git restore --source <commit> --worktree <file>` : Restore working directory `<file>` from `<commit>`, usually HEAD

`revert`
- `git revert <commit>` : Create a new commit that revert the change made in `<commit>`

# History

`reset` 
Reset move the branch that HEAD is pointing to. 
`git reset <commit>`
    - `--soft`  : Update just the branch; the staging area is untouched, it still contain a copy of your last commit and everything you staged after
    - `--mixed` : Update the branch then the index; everything has been unstaged
    - `--hard`  : Update the branch, the index, and then the working directory
`git reset <commit> <file>` : Copy `<file>` as it was in `<commit>` to the index
    - `(--patch | -p)`           : Partially reseting a file


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
- merge ?
- `(-r|--rebase)`
- fast-foward ?

`git push`

# Others

`git tag`