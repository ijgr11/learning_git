# Git - Undoing Things

## What is HEAD?

> The HEAD in Git is the **pointer** to the current branch reference, which is in turn a pointer to the last commit you made. It's generally simplest to think of it as HEAD is the snapshot of your last commit.
> HEAD is not a commit; it points to one, points to the last commit.

To confirm that HEAD poinst to the last commit we can run:
`git show HEAD`

Output:

```sh
commit e4faa68b9db12e48d393ed29f34cdb0fa1b928ef (HEAD -> master)
Author: Isma <ijgr11@gmail.com>
Date:   Wed Oct 28 00:20:01 2020 -0600

    Created new file for chapter 3

diff --git a/git_undoing_things.md b/git_undoing_things.md
new file mode 100644
index 0000000..e69de29
```

We can also see details for other commits:
`git show HEAD~1` - shows the second commit (the first one is 0 which is the latest one.)
`git show e4faa68b9db12e48d393ed29f34cdb0fa1b928ef` - shows details for the commit with that ID.

To get a history of all of the places HEAD has pointed you can run:
`git reflog HEAD`

Output:

```sh
e4faa68 (HEAD -> master) HEAD@{0}: commit: Created new file for chapter 3
4663d30 HEAD@{1}: commit: Adding check git history
ce27a67 HEAD@{2}: commit: Changed format and added subtitles
69e7d57 HEAD@{3}: commit: added results from git status
6991290 HEAD@{4}: commit: Added new info for each status
c0018cb HEAD@{5}: commit (initial): Initial Commit
```

## Git Checkout

We can _unmodify_ files also we can _"go back in time"_ and check different states of our project, we can also move between branches.

### UnModifying Files

Lets say we modified file test.txt, and added text "Error #2"

```sh
Change #1
Error #2
```

But we realized there was an error with or last change ("Error #2") and we need to revert that, in order to revert these changes we run:

`git checkout test_file1.txt`

### _"Going back in time"_

With `git checkout <file>` we can _"go back in time"_ and check the previous states of the project, unlike other commants like `git revert` and `git reset`, `git checkout` is the **safest** one because with it we cannot change or delete previous commits.

Lets say we added new texts to our test_file:

```sh
Adding text: "Change #1"
Adding text: "Change #2"
Adding text: "Change #3"
Adding text: "Error #4"
```

Checking at the history of changes `git log --oneline`, it returns:

```sh
git log --oneline
b47ba1e (HEAD -> master) test_file1 -- Adding text: "Error #4"
75105a4 test_file1 -- Adding text: "Change #3"
d8fd895 test_file1 -- Adding text: "Change #2"
855a5f5 test_file1 -- Adding text: "Change #1"
```

We realize we need to go back in time to "Change #3", we can run:

`git checkout 75105a4`
Output:

```sh
Note: switching to '75105a4'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at 75105a4 test_file1 -- Adding text: "Change #3"
```

If we check the `git log` we will see that the HEAD is currently at the _Change #3_ commit.

```sh
git log --oneline
75105a4 (HEAD) test_file1 -- Adding text: "Change #3"
d8fd895 test_file1 -- Adding text: "Change #2"
855a5f5 test_file1 -- Adding text: "Change #1"
```

If we want to go back to the master branch or the latest commit we run:
`git checkout master`
Output:

```sh
M       git_undoing_things.md
Previous HEAD position was 75105a4 test_file1 -- Adding text: "Change #3"
Switched to branch 'master'
```

And now the `git log` shows the HEAD at the latest commit:

```sh
b47ba1e (HEAD -> master) test_file1 -- Adding text: "Error #4"
75105a4 test_file1 -- Adding text: "Change #3"
d8fd895 test_file1 -- Adding text: "Change #2"
855a5f5 test_file1 -- Adding text: "Change #1"
```

### `git checkout` is READ ONLY

`git checkout` is very safe because it is a **Read Only**, you cannot change or edit previous commits.

If we go back in time to a previous commit, make changes to it, stage them and then commit them, and then we go to master again this change we just made will be erased because, again, checkout is only for **Read Only**, and experimental tests, meaning you can make the change to previous commit, you can test them and see how they work but they will never be saved.

Let's see a test:

Here are new commits:

```sh
~ git log --oneline

3a4eba6 (HEAD -> master) test_file1 -- Adding text: "Error #8"
dcb27ce test_file1 -- Adding text: "Change #7"
f6bd178 test_file1 -- Adding text: "Change #6"
2ff9388 test_file1 -- Adding text: "Change #5"
b47ba1e test_file1 -- Adding text: "Error #4"
75105a4 test_file1 -- Adding text: "Change #3"
d8fd895 test_file1 -- Adding text: "Change #2"
855a5f5 test_file1 -- Adding text: "Change #1"
```

Lets "go back" to "Change #7" by running `git checkout dcb27ce`

```sh
git log --oneline
dcb27ce (HEAD) test_file1 -- Adding text: "Change #7"
f6bd178 test_file1 -- Adding text: "Change #6"
2ff9388 test_file1 -- Adding text: "Change #5"
b47ba1e test_file1 -- Adding text: "Error #4"
75105a4 test_file1 -- Adding text: "Change #3"
d8fd895 test_file1 -- Adding text: "Change #2"
855a5f5 test_file1 -- Adding text: "Change #1"
```

Nice, now lets make a change to the current commit we are on, on test_file we are removing some lines and adding new ones:

current file:

```sh
Adding text: "Change #1"
Adding text: "Change #2"
Adding text: "Change #3"
Adding text: "Error #4"
Adding text: "Change #5"
Adding text: "Change #6"
Adding text: "Change #7"
```

new changes:

```sh
Adding text: "Change #1"
Adding text: "Change #2"
Adding text: "Change #3"
THIS ARE CHANGES TO CONFIRM CHANGES WILL NOT BE SAVED.
```

Lets see the `git status`:

```sh
HEAD detached at dcb27ce
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   test_file1.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Ok we see changes, lets stage them and then commit them:

```sh
git add test_file1.txt

git status
HEAD detached at dcb27ce
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   test_file1.txt

git commit -m 'Committing changes that wont be saved'
[detached HEAD e40ac3e] Committing changes that wont be saved
 1 file changed, 1 insertion(+), 4 deletions(-)

git status
HEAD detached from dcb27ce
nothing to commit, working tree clean
11:36:03 - isman

git log --oneline
e40ac3e (HEAD) Committing changes that wont be saved
dcb27ce test_file1 -- Adding text: "Change #7"
f6bd178 test_file1 -- Adding text: "Change #6"
2ff9388 test_file1 -- Adding text: "Change #5"
b47ba1e test_file1 -- Adding text: "Error #4"
75105a4 test_file1 -- Adding text: "Change #3"
d8fd895 test_file1 -- Adding text: "Change #2"
855a5f5 test_file1 -- Adding text: "Change #1"
```

Now, lets go to the master branch once again:

```sh
git checkout master
Warning: you are leaving 1 commit behind, not connected to
any of your branches:

  e40ac3e Committing changes that wont be saved

If you want to keep it by creating a new branch, this may be a good time
to do so with:

 git branch <new-branch-name> e40ac3e

Switched to branch 'master'
```

Checking the history returns no commit for the change we just made:

```sh
git log --oneline
3a4eba6 (HEAD -> master) test_file1 -- Adding text: "Error #8"
dcb27ce test_file1 -- Adding text: "Change #7"
f6bd178 test_file1 -- Adding text: "Change #6"
2ff9388 test_file1 -- Adding text: "Change #5"
b47ba1e test_file1 -- Adding text: "Error #4"
75105a4 test_file1 -- Adding text: "Change #3"
d8fd895 test_file1 -- Adding text: "Change #2"
855a5f5 test_file1 -- Adding text: "Change #1"
```

## Git Revert

> The "revert" command helps you undo an existing commit.
> It's important to understand that it does not delete any data in this process: instead, Git will create new changes with the opposite effect - and thereby undo the specified old commit.
> The `git revert` command is used to ‘undo’ the changes you have made in the past. Simple. But unlike other undo commands, git revert will introduce a new commit that has the inverted changes.

For example:

## Git Revert

> The "revert" command helps you undo an existing commit.
> It's important to understand that it does not delete any data in this process: instead, Git will create new changes with the opposite effect - and thereby undo the specified old commit.
> `git revert` goes back in time and revert an specific commit but the rest of the commits stay the same.
> The `git revert` command is used to ‘undo’ the changes you have made in the past. Simple. But unlike other undo commands, git revert will introduce a new commit that has the inverted changes.

For example:

```sh
git log --oneline
62afdae (HEAD -> master) Added file test_file2
0c9cf4b Adding text: "Change #4"
e27ab48 Adding text: "Error #3"
1a50004 Adding text: "Change #2"
834ec2b Adding text: "Change #1"
```

Reverting the changes:

```sh
git revert e27ab48

[master 132c826] Revert "Adding text: "Error #3""
 1 file changed, 1 insertion(+), 2 deletions(-)
```

The result is:

```sh
git log --oneline
132c826 (HEAD -> master) Revert "Adding text: "Error #3""
62afdae Added file test_file2
0c9cf4b Adding text: "Change #4"
e27ab48 Adding text: "Error #3"
1a50004 Adding text: "Change #2"
834ec2b Adding text: "Change #1"
```

Now the test_file1 displays:

```sh
Adding text: "Change #1"
Adding text: "Change #2"
```

Instead of:

```sh
Adding text: "Change #1"
Adding text: "Change #2"
Adding text: "Error #3"
Adding text: "Change #4"
```

And the file test_file2 is still there.

If there is a change that conflicts with other changes we will be presented with a warning:

```sh
git revert 66e81a0
Auto-merging test_file1.txt
CONFLICT (content): Merge conflict in test_file1.txt
error: could not revert 66e81a0... Fixed Adding text: "Change #3"
hint: after resolving the conflicts, mark the corrected paths
hint: with 'git add <paths>' or 'git rm <paths>'
hint: and commit the result with 'git commit'
```

And will need to take an action

```sh
Accept Current Change | Accept Incoming Change | Accept Both Changes | Compare Changes

Adding text: "Change #1"
<<<<<<< HEAD
Adding text: "Change #2"
Adding text: "Change #3"
Adding text: "Change #4"
Adding text: "Change #5"
Adding text: "Change #6"
=======
Adding text: "Change #2"
>>>>>>> parent of 66e81a0... Fixed Adding text: "Change #3"
```

If we want t avoid the revert operation we can cancel it by running `git revert --abort` and it will go back to the latest commit.

## Git Reset

This is a very dangerous command if not used wisely, this command will actually delete commits from the history.

### Git Reset Soft

The difference between mixed and soft is that with soft the changes are not removed from staging area immediately.

Lets see the history of commits:

```sh
git log --oneline
bd20f70 (HEAD -> master) Removed Change 3 and Change 4 from test_file1
d9a06a8 Added Change 5 and 6 into test1 and Change 1 and 2 into test2
66e81a0 Fixed Adding text: "Change #3"
132c826 Revert "Adding text: "Error #3""
bd0c153 changes on test_file1
62afdae Added file test_file2
0c9cf4b Adding text: "Change #4"
e27ab48 Adding text: "Error #3"
1a50004 Adding text: "Change #2"
834ec2b Adding text: "Change #1"
```

Lets reset the second "Change #3"
`git reset --soft 66e81a0`

The new commit history looks like this:

```sh
git log --oneline
66e81a0 (HEAD -> master) Fixed Adding text: "Change #3"
132c826 Revert "Adding text: "Error #3""
bd0c153 changes on test_file1
62afdae Added file test_file2
0c9cf4b Adding text: "Change #4"
e27ab48 Adding text: "Error #3"
1a50004 Adding text: "Change #2"
834ec2b Adding text: "Change #1"
```

The result of soft reset is to remove all the commits from the history but left the changed files in the staging area:

```sh
git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   test_file1.txt
        modified:   test_file2.txt
```

To unstage the changes

`git reset .`

```sh
git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   test_file1.txt
        modified:   test_file2.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

To accept these changes:

`git checkout .`

### Git Reset Mixed

`git reset --mixed <id>` will remove the commits from history however it will not remove the actually changes from the files, but will unstage them, contrary to `git reset --soft <id>` which will keep the files in the stage area.

Lets see where we are right now:

```sh
git log --oneline
66e81a0 (HEAD -> master) Fixed Adding text: "Change #3"
132c826 Revert "Adding text: "Error #3""
bd0c153 changes on test_file1
62afdae Added file test_file2
0c9cf4b Adding text: "Change #4"
e27ab48 Adding text: "Error #3"
1a50004 Adding text: "Change #2"
834ec2b Adding text: "Change #1"
```

Lets reset to "Change #4"

```sh
git reset --mixed 0c9cf4b
Unstaged changes after reset:
M       test_file1.txt
```

As we can see the commits are deleted but also the changes are unstaged

```sh
git log --oneline
0c9cf4b (HEAD -> master) Adding text: "Change #4"
e27ab48 Adding text: "Error #3"
1a50004 Adding text: "Change #2"
834ec2b Adding text: "Change #1"
```

```sh
git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   test_file1.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test_file2.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

To accept the changes:
`git checkout .`

In the case of also removing a created file:

```sh
git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        test_file2.txt

nothing added to commit but untracked files present (use "git add" to track)
```

To check which file will be removed:

```sh
git clean -n
Would remove test_file2.txt
```

To remove that file:

```sh
git clean -f
Removing test_file2.txt
```

### Git Reset Hard

`git reset --hard <id>` will remove the commits from history, and apply the changes automatically (pretty much a hard wipe out).

**ONLY USE IT IF YOU ARE SURE YOU NEED TO CLEAN SUCH CHANGES**

## Git Ignore

Helps in order to ignore files that we dont want to include in our commits.

It requires a file `.gitignore` to be created and within it we need to include the name of the file, path or regex that we want to ignore.

```sh
/file1.txt
path1/file2.txt
path2/*.css
path3/*

# we can also make comments
```

If we need to ignore a file that was previously created (before the `.gitignore`) we need to clear the cache from the history:

`git rm -r --cached .`

Then files must be unstaged and then removed (as explained before.)
