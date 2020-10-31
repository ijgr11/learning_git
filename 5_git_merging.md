# Git Merging Branches

Merging Branches is the process of combining branches with the master branch.

## Fast-Forward Merge

This is a "linear timeline", this means, the new branch was created based on the last commit of the master branch and while working on the new branch there were not actual change in the master branch.

![fast-forward](<https://wac-cdn.atlassian.com/dam/jcr:b87df050-2a3a-4f17-bb80-43c5217b4947/07%20(1).svg>)

Once both branches are merged, and master branch will adquire all changes applied in the new branch.

Merge must be done from master branch with command:

`git merge <name_branch>`

Output:

```sh
git merge dev
Updating 60e6083..7b0a231
Fast-forward
 test_file1.txt | 4 +++-
 1 file changed, 3 insertions(+), 1 deletion(-)
```

When both branches have the same files/changes, the history looks like this:

`(HEAD -> feature, master)`

```sh
git log --oneline
1254c21 (HEAD -> dev, master) handling merge aborts
a2d29d2 (origin/master) Adding notes for Merge conflicts
0d9336b Adding notes for Merge conflicts
```

## 3-way Merge

This happens when aftter we created a new branch and worked on it, someone else also made changes to the master branch before we merge the branch and master branch

![3-way](https://wac-cdn.atlassian.com/dam/jcr:91b1bdf5-fda3-4d20-b108-0bb9eea402b2/08.svg?cdnVersion=1319)

```sh
git merge dev
Merge made by the 'recursive' strategy.
 test_file1.txt | 4 +++-
 1 file changed, 3 insertions(+), 1 deletion(-)
```

Status of the commit history:

```sh
git log --oneline
7667ab2 (HEAD -> master) Merge branch 'dev'
237209f (dev) Created Error 8
c0089fd Created Error 7
```

## Merge conflicts

When there are conflicts git will let us know about that and ask us to chose which change is the one we want to keep.

```sh
Accept Current Change | Accept Incoming Change | Accept Both Changes | Compare Changes
<<<<<<< HEAD (Current Changes)
[MASTER]Adding text: "Change #9"
=======
[DEV]Adding text: "Change #9"
>>>>>>> dev (Incoming Change)
```

In case there is a conflict and we dont want to continue with the merge:

```sh
git merge dev
Auto-merging 5_git_merging.md
CONFLICT (content): Merge conflict in 5_git_merging.md
Automatic merge failed; fix conflicts and then commit the result.
```

We can cancel it by running:

`git merge --abort`

## Git Rebase

Git rebase is used to integrate changes from one branch into another.

In other words, it is the process of moving or combining a sequence of commits to a new base commit.

![git_rebase](https://wac-cdn.atlassian.com/dam/jcr:e4a40899-636b-4988-9774-eaa8a440575b/02.svg)

In order to sync the last commit from master into the feature branch we run from the feature branch:

```sh
git rebase master
First, rewinding head to replay your work on top of it...
Fast-forwarded feature to master.
```

Important:

If we make a change in the master branch, and then change and commit to "feature" branch and make a change there and commit, and then we want to sync everything.

We need to first rebase the master branch into the feature branch:

```sh
[feature]$ git rebase master
First, rewinding head to replay your work on top of it...
Applying: Added Change 10
```

Then once the "feature" branch has been updated/rebased we can change to the master branch and merge commits from feature branch:

```sh
git checkout master
Switched to branch 'master'

git merge feature
Updating 116a0ba..84e4774
Fast-forward
 test_file1.txt | 1 +
 1 file changed, 1 insertion(+)
```

This will create a fast-forward merge because we are updating feature branch with the latest changes from master branch and then from there adding/merging the changes from feature branch into master branch making them both have the same commits.
