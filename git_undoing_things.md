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
