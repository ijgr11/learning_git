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
```sh
From https://github.com/user/repo.git
*  branch   master -> FETCH_HEAD
Updating 642592f...fc68b22
Fast-forward
 3_git_github.md | 1 +
 1 file changed, 1 insertion(+)
```
We can also pull data from the remote repo in a shorter way, we might just need to set the following command:
`git branch --set-upstream-to=origin/master master`

The first master is the branch of our repo on github, the second master is the default branch in the local repo.
