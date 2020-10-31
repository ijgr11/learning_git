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

## Deleting branches

To delete branch locally:

`git branch -d localBranchName`

To delete branch remotely:

`git push origin --delete remoteBranchName`
