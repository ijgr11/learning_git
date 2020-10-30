# Github

## From Local to Github

1. Connect to Github:

   `git remote add <remote_repo_name> <link_remote_repo>`

2. Pushing to Github:

   `git push <remote_repo_name> <name_working_branch>`

   since we are working in the master branch, thats the one we will use for now.
   for example:

   `git push origin master`

   Output:

   ```sh
   git push origin master
   Username for 'https://github.com': <github_username>
   Password for 'https://<github_username>@github.com': <github_password OR token>
   Enumerating objects: 76, done.
   Counting objects: 100% (76/76), done.
   Delta compression using up to 4 threads
   Compressing objects: 100% (65/65), done.
   Writing objects: 100% (76/76), 12.46 KiB | 1.13 MiB/s, done.
   Total 76 (delta 30), reused 0 (delta 0)
   remote: Resolving deltas: 100% (30/30), done.
   To https://github.com/user/repo.git
   * [new branch]      master -> master
   ```

## From Github to Local

Lets say we made a change in Github or any other remote place and it got updated on Github but not in our local repo (this change is made in github btw).

We can sync this change into our local repo by running:

`git push <remote_repo_name> <name_working_branch>`

for example:

`git pull origin master`

Output:

```
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (3/3), done.
remote: Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/ijgr11/learning_git
 * branch            master     -> FETCH_HEAD
   eb2a217..3370c00  master     -> origin/master
Updating eb2a217..3370c00
Fast-forward
 3_git_github.md | 22 ++++++++++++++++++++++
 1 file changed, 22 insertions(+)
```

We can also pull data from the remote repo in a shorter way, we might just need to set the following command:

`git branch --set-upstream-to=origin/master master`

The first master is the branch of our repo on github, the second master is the default branch in the local repo.

```sh
git log --oneline

3370c00 (HEAD -> master, origin/master) Updated the 3_git_github.md
eb2a217 Added README.md File
56591d9 Updated git_basics with git mv
3e29771 Changed names for files
8a1846a Added git_github file
```
