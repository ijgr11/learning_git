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

## 3-way Merge

This happens when aftter we created a new branch and worked on it, someone else also made changes to the master branch before we merge the branch and master branch
<<<<<<< HEAD
=======

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
>>>>>>> dev
