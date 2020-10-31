# Git Branch

If we think of Git as a timeline of our projects then Branches are alternate universes or alternate timelines where we can make changes to the main project but without affecting it.

If we are happy with the changes we made in our branch then we can merge it with the master branch.

Branches also allow multiple collaborators to work on multiple features, fixes, improvements, etc in the project without breaking the main code or conflicting with other collaborators.

![branching](https://camo.githubusercontent.com/40d55b046f0d99b8fa90d6518424294ddcd0c003/68747470733a2f2f7777772e61746c61737369616e2e636f6d2f64616d2f6a63723a39663134396365662d663738342d343364652d383230372d3365373936383738396131662f30332e737667)

In order to **create a new branch** we run command `git branch <branch name>`.

And in order to check how many branches are created we run `git branch` which returns:

```sh
* master
  test_branch
```

In order to switch to a different branch we run `git checkout <branch name>`.

```sh
git checkout test_branch

Switched to branch 'test_branch'
```

And running again `git branch` will return:

```sh
* test_branch
  master
```

If we run `git log --oneline` on the new branch, it will show all commit history as the ones in the master branch at the moment of the creation of the new branch:

```sh
git log --oneline
a730213 (HEAD -> test_branch) Updates on Document
1a68236 General formatting fixes
3bbc35a Update format 3_git_github
4717a45 Update 3_git_github & added 4_git_branch
3370c00 Updated the 3_git_github.md
```

After making changes and committing them in the new branch, we can see that this new branch is one commit ahead of the master branch

```sh
git log --oneline
a19baa8 (HEAD -> test_branch) Added Change#5 and 6
8054a4b (origin/master, master) Update to 4_git_branching
```

In order to push the new branch to the GitHub repo we need to run:

`git push origin <branch_name>`

```sh
git push origin test_branch
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 4 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 290 bytes | 290.00 KiB/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
remote:
remote: Create a pull request for 'test_branch' on GitHub by visiting:
remote:      https://github.com/ijgr11/learning_git/pull/new/test_branch
remote:
To https://github.com/ijgr11/learning_git.git
 * [new branch]      test_branch -> test_branch
```

Branches created from GitHub can also be pulled into local repo, just run:

`git pull origin <name_new_remote_branch>`

```sh
git pull origin test_branch2
From https://github.com/ijgr11/learning_git
 * branch            test_branch2 -> FETCH_HEAD
 * [new branch]      test_branch2 -> origin/test_branch2
Already up to date.
```

Then run `git checkout --track origin/<name_new_remote_branch>`

```sh
git checkout --track origin/test_branch2
Branch 'test_branch2' set up to track remote branch 'test_branch2' from 'origin'.
Switched to a new branch 'test_branch2'
```

Check the list of all branches:

```sh
git branch
  master
  test_branch
* test_branch2
```

If we made a change to the test_branch2 in GitHub, we can pull that into our local repo by running `git pull origin <remote_new_branch>`:

```sh
git pull origin test_branch2
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/ijgr11/learning_git
 * branch            test_branch2 -> FETCH_HEAD
   8054a4b..42b1fed  test_branch2 -> origin/test_branch2
Updating 8054a4b..42b1fed
Fast-forward
 test_file2.txt | 2 ++
 1 file changed, 2 insertions(+)
 create mode 100644 test_file2.txt
```

To create a branch and move to it automatically with just one command, we can run:

`git checkout -b <branch_name>`

## Deleting branches

You cannot delete branches you are currently on.

To delete branch locally:

`git branch -d localBranchName`

OR use -D option

```sh
git branch -d test_branch
error: The branch 'test_branch' is not fully merged.
If you are sure you want to delete it, run 'git branch -D test_branch'.
```

To delete branch remotely:

`git push origin --delete remoteBranchName`

Example:

```sh
git push origin --delete test_branch
To https://github.com/ijgr11/learning_git.git
 - [deleted]         test_branch
```
