# Git

## Initialize the Directory

Within the directory to work on enter the following command:
`git init`

To display the .git folder on VSCode just edit the settings by changing exclude value for git from _true_ to _false_.
`"\*\*/.git": false,`

Once the directory has been initial we can check the status of the commits.
`git status`

Which returns the following output:

```sh
On branch master
No commits yet
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        .python-version
        index.html
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

Initial status of a file is **Untracked**

| Untracked  | Modified | Staged | Committed |
| ---------- | -------- | ------ | --------- |
| index.html |          |        |           |

In order to track a file we use:
`git add <file name>`

After running that command the file goes from **Untracked** to **Staged**, files under the staging area means these files are ready to be **Committed**.

| Untracked | Modified | Staged     | Committed |
| --------- | -------- | ---------- | --------- |
|           |          | index.html |           |

In order to commit a file we run:
`git commit -m "Initial Commit"`

| Untracked | Modified | Staged | Committed  |
| --------- | -------- | ------ | ---------- |
|           |          |        | index.html |

If the file is modified after being tracked (committed) then it will be changed to **Modified**

| Untracked | Modified   | Staged | Committed |
| --------- | ---------- | ------ | --------- |
|           | index.html |        |           |

From here it can be staged again and then committed.
