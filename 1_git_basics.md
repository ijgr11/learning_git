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

## [Git Three States](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F#_the_three_states)

Pay attention now — here is the main thing to remember about Git if you want the rest of your learning process to go smoothly. Git has three main states that your files can reside in: **modified**, **staged**, and **committed**:

- Modified means that you have changed the file but have not committed it to your database yet.

- Staged means that you have marked a modified file in its current version to go into your next commit snapshot.

- Committed means that the data is safely stored in your local database.

This leads us to the three main sections of a Git project: the working tree, the staging area, and the Git directory.

![three states](https://git-scm.com/book/en/v2/images/areas.png)

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

To add the file to staging area AND commit it as well we run:

`git commit -am 'Message'`

It only work for modified or deleted files, but if there are new files not tracked then it will not work.

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

In order to check the history of the commits we run:

`git log`

Which returns:

```sh
commit e4faa68b9db12e48d393ed29f34cdb0fa1b928ef (HEAD -> master)
Author: Isma <ijgr11@gmail.com>
Date:   Wed Oct 28 00:20:01 2020 -0600

    Created new file for chapter 3

commit 4663d3084b105ac8b35f085428e45532e38dbc51
Author: Isma <ijgr11@gmail.com>
Date:   Wed Oct 28 00:18:37 2020 -0600

    Adding check git history

commit c0018cb08a616e1aa264963ba80d0a55071e9c08
Author: Isma <ijgr11@gmail.com>
Date:   Tue Oct 27 23:42:54 2020 -0600

    Initial Commit
```

We can also have this info in a summarized way:

`git log --oneline`

Which returns:

```sh
e4faa68 (HEAD -> master) Created new file for chapter 3
4663d30 Adding check git history
c0018cb Initial Commit
```

A more detailed and "graphic" way to represent the same:

```sh
git log --oneline --decorate --graph --all
* a313842 (HEAD -> master, origin/master) Git diff udpates
* 0526097 Git diff examples update
* fa2b03b Git diff examples
* df4c08e Updated protecting branches
* a6eb20b Updated 6_git_forking
*   09213bf Merge branch 'master' of https://github.com/ijgr11/learning_git
|\
| *   f264e69 Merge pull request #2 from ijgr11/test
| |\
| | *   dcf63e4 Merge branch 'master' into test
| | |\
| | |/
| |/|
| * | 53a48b0 Updated [GITHUB] Adding text: "Change #15" -Master
| | * 104823f Updated [GITHUB] Adding text: "Change #14"
| | * a5ffdc4 Added [GITHUB] Adding text: "Change #13"
| |/
| *   7521697 Merge pull request #1 from ijgr11/feature-1
| |\
| | * 2a2a9a7 [GITHUB] Adding text: "Change #12"
| | * ee0e7f8 Adding text: "Change #11"
| |/
* | fe55646 add 6_git_forking
|/
* 8f977e3 rebase from 5_git to feat and them merged
* 84e4774 Added Change 10
* 116a0ba Added rebase to 5_git
* 5ab6874 Updates on git 5
* 1254c21 handling merge aborts
* a2d29d2 Adding notes for Merge conflicts
* 0d9336b Adding notes for Merge conflicts
*   57fb8ca Merge branch 'dev'
|\
| * 6d4ff2a Added Change #9
* | 12a2fa0 Added Change #9 on master
|/
* 0aef167 Merge Conflict
* 5922bbe Updated documentation
*   af406c4 Updated git 5
|\
| * 3fa481a Added info for 3-way
* |   7667ab2 Merge branch 'dev'
|\ \
| |/
| * 237209f Created Error 8
| * c0089fd Created Error 7
* | 7c2ccd2 Updated git 1 and git 5
* | ce2fa13 Created 5_git_merging
|/
* 7b0a231 Added Change #6 to test_file1
```

## Git Changing/Moving Names to files/folders

In order to change name to a file or folder or to move it to a different location do not change it directly to the file, instead use:

`git mv old_name new_name`

for example:

```sh
git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    old_name -> new_name
```

We can automatically commit after this if we desire:

```sh
git commit -m 'Changed names for files'
[master 3e29771] Changed names for files
 3 files changed, 0 insertions(+), 0 deletions(-)
 rename old_name => new_name (100%)
```

## Git Diff, comparing changes.

In order to track the difference between the changes made on a file.

```sh
git diff
diff --git a/test_file1.txt b/test_file1.txt
index f290e76..498d265 100644
--- a/test_file1.txt
+++ b/test_file1.txt
@@ -14,3 +14,4 @@ Adding text: "Change #8"
 [GITHUB] Adding text: "Change #13"
 [GITHUB] Adding text: "Change #14"
 [GITHUB] Adding text: "Change #15"
+[LOCAL] Adding text: "Change #16"
\ No newline at end of file
```

Explained:

![git_diff](https://www.toolsqa.com/wp-content/gallery/git/git_diff_command.png)

> Note: Diff Command will produce the changes in all the files that are present. For the changes on some specific files only, type the name of the file after the command name.
>
> Let’s see now how git diff command responds to the operations we just did.
>
> Now let us breakdown the response given by git diff and understand everything one by one.
>
> 1. The first line shows the file names that have been considered as the input in git diff. You can see that they have been marked by a and b along with the two different file state that has been taken as input.
> 2. This line is not of use. This shows the metadata related to the command and the execution of it on the files. As you must be aware by our discussion in Dot Git folder, this is the object hash value required by Git for internal use.
> 3. This line defines the symbol, called a legend, to tell you what is used to describe the first file and what is used to describe the second file. As you can see, – is used in front of the first file and + is used in front of the second file. So whenever diff shows you the changes related to the first file, they will be marked by – and the changes in the second file will be marked by the symbol +.
> 4. The fourth line shows you symbol @@ and symbols ahead of it. They are called chunks. Chunks in git diff define the change’ summary. In our image below the following chunk can be seen @@ -1,2 +1 @@
> 5. This means that line one and two were changed in the first file and line one was changed in the second file. Remember the – and + symbol used in the third point to as a symbol to the first and second file respectively.

Ref [Git-Diff](https://www.toolsqa.com/git/git-diff/)
