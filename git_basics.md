# Git - Basics

## Initializing the Directory

In order to start using Git we need to initialize the project.
Within the directory to work on, enter the following command:
`git init`

**NOTE**: To display the .git folder on VSCode just edit the settings by changing exclude value for git from _true_ to _false_. `"\*\*/.git": false,`

Once the directory has been initial we can check the status of the commits.
`git status`

Which returns the following output:

```sh
On branch master
No commits yet
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .python-version
        git_basics.md
nothing added to commit but untracked files present (use "git add" to track)
```

Whenever we are unsure about what's the right syntaxt for git commands or what options do we have for a given git command we can type the command plus **--help**, for example:

`git status --help`

```sh
GIT-STATUS(1)					Git Manual					GIT-STATUS(1)
NAME
       git-status - Show the working tree status
SYNOPSIS
       git status [<options>...] [--] [<pathspec>...]
...
```

## Git File Status

From [Git Basics - Recording Changes to the Repository](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository#:~:text=Untracked%20files%20are%20everything%20else,not%20in%20your%20staging%20area.&text=As%20you%20edit%20files%2C%20Git,them%20since%20your%20last%20commit.):

> Remember that each file in your working directory can be in one of two states: _tracked_ or _untracked_.
> **Tracked** files are files that were in the last snapshot; they can be unmodified, modified, or staged. In short, tracked files are files that Git knows about.
> **Untracked** files are everything else — any files in your working directory that were not in your last snapshot and are not in your staging area.
> When you first clone a repository, all of your files will be tracked and unmodified because Git just checked them out and you haven’t edited anything.

![alt text](https://git-scm.com/book/en/v2/images/lifecycle.png)

### Untracked

| Untracked  | Modified | Staged | Committed |
| ---------- | -------- | ------ | --------- |
| index.html |          |        |           |

So, remember, the initial status of a file is **Untracked**

### Staged

| Untracked | Modified | Staged     | Committed |
| --------- | -------- | ---------- | --------- |
|           |          | index.html |           |

In order to start tracking a file we use:
`git add <file name>`

Which returns the following output:

```sh
On branch master
No commits yet
Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   git_basics.md
```

After running that command the file goes from **Untracked** to **Staged**, files under the staging area means these files are ready to be **Committed**.

### Committed

| Untracked | Modified | Staged | Committed  |
| --------- | -------- | ------ | ---------- |
|           |          |        | index.html |

This is the final phase, in order to commit a file we run:
`git commit -m "Initial Commit"`

Which returns the following output:

```sh
[master (root-commit) c0018cb] Initial Commit
 1 file changed, 81 insertions(+)
 create mode 100644 git_basics.md
```

git status returns:

```sh
On branch master
nothing to commit, working tree clean
```

### Modified

| Untracked | Modified   | Staged | Committed |
| --------- | ---------- | ------ | --------- |
|           | index.html |        |           |

If the file is modified after being tracked (committed) then it will be changed to **Modified**

```sh
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   git_basics.md

no changes added to commit (use "git add" and/or "git commit -a")
```

From here it can be staged again and then committed.

### Unstaging

| Untracked  | Modified | Staged | Committed |
| ---------- | -------- | ------ | --------- |
| index.html |          |        |           |

In case we committed a mistage and want to remove a file from the **\*Staged** area we can run the following command:
`git rm --cached <file>`

Which returns:
`rm 'git_basics.md'`

And status:

```sh
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    git_basics.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        git_basics.md
```

Also `git restore --staged <file>...` can be used to unstage changes, but most accurate it is used to move to the previous status:

```sh
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   git_basics.md

no changes added to commit (use "git add" and/or "git commit -a")
```

## Your First commit?

In your first commit you will need to identify yourself:

```sh
git config --global user.name Your Name
git config --global user.email Your@email.com
```

To check the settings just run:

```sh
git config --global user.name
git config --global user.email
```

## Check History
