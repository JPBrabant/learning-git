# Help

`git help <command>`


# Creating a repository

`git init`

`git clone`


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

`grep`
Search inside the working directory, the index or the repo. There is a lot of available options.
- `git grep <search-pattern> <commit>`

`git diff`
- `--name-only`
- `--cached|--staged`

`ls-files`
- `git ls-files`        : Show all filed tracked by git
    - `(-s|--stage)`    : Show files in the index
    - `(-u|--unmerged)` : In case a merge failed, show 3 version of the same file where 1. common ancestor, 2. ours changes, 3. theirs changes


# Commiting

Commiting is the act of saving a snapshot of your code. The process consist of staging your changes and then commiting. When you commit, a snapshot of the index is saved. The index start as a copy of everything that was saved in a commit, and the index is updated with `add`, `rm` and `mv`. 

`add`
Updates the index using the current content found in the working tree, to prepare the content staged for the next commit. The index holds a snapshot of the content of the working tree, and it is this snapshot that is taken as the contents of the next commit. Everyting you add will be saved in the object database of git and can be restored.
-`git add <pathspec>...`   : Stage a file.
    - `(-p|--patch)`       : Allow you to stage part of a file (hunk).
-`git add`                 : Stage all files in the current directory (new files YES, modifications YES, deletions NO).
    - `(-u|--update)`      : Stage all files in the current directory (new files NO,  modifications YES, deletions YES).
    - `(-A|--all)`         : Stage all files in the current directory (new files YES, modifications YES, deletions YES).
    - `(-i|--interactive)` : Allow you to choose what files to add from a list.

`rm`
Remove files from the index, or from the working tree **AND** the index. The next commit will show the file deleted, that tell git to stop tracking the file.
- `git rm <pathspec>...` : Removes the file from the index and deletes it from the working directory.
    - `--cached`         : Removes the file from the index but keep it on disk as an untracked file.
    - `(-f|--force)`     : Necessery if the file was never tracked by git (the file will be unrecoverable).
    - `-r`               : To recurse inside a folder.

`mv`
- `git mv <source> <destination>` : Move or rename a file or directory.

`commit`
Create a new commit containing the current contents of the index. After commiting, git will check at what branch HEAD is pointing, and move this branch to the new commit. In detached HEAD, HEAD is moved itself to point to the new commit.
Though not required, it's a good idea to begin the commit message with a single short (no more than 50 characters) line summarizing the change, followed by a blank line and then a more thorough description. 
- `git commit`   : Commit the current state of the index. An editor will open to allow you to write a commit message. 
    - `--ammend` : Overwrite the last commit with the current state of the index.


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
Git change where HEAD is pointing and try to update both the working directory and the index with the content of the commit. If you have uncomited change that would conflit, the command abort. 
- `git switch <branch>`                      : Move HEAD to a branch (`-` shortcut for the previous branch)
    - `(-c|--create)`                        : Create and switch branch
- `git switch (-d|--detached) <start-point>` : Used for detached HEAD (switch to a specific commit or a remote branch because you can't edit a remote branch)

`merge`
- `git merge <commit>`             : Incorporates changes from the named commits (since the time their histories diverged) into the current branch
    - *Fast-foward*                : If the current branch is an ancestor of `<commit>`, current branch will simply move
- `git merge (--continue|--abort)` : Fix merge conflict and then continue (you need to tell git that the conflict has been resolved with `git add`) or abort

`rebase`
- `git rebase <destination-branch>` : Move changes from HEAD (since the time their histories diverged) to `<destination-branch>`
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

`clean`
Cleans the working tree by recursively removing files that are not under version control (like temporary build artifacts or merge conflict files).
- `git clean`           : Remove untracked files in your working repository.
    - `-d`              : Include untracked directories
    - `-x`              : Include ignored files (files in .gitignore)
    - `(-n|--dry-run)`  : See what it will delete
    - `(-f|--force)`    : Confirm the delete operation