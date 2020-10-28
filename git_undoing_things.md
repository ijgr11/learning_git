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
