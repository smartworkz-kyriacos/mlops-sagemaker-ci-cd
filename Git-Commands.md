# Top 30 Git Commands

In this article, we list the most essential commands that one should know as a developer and become a master in handling their GitHub repositories. Beginners and experienced developers can benefit from this article.

1. Set Up Your Username and Email
2. Cache Your Login Credentials
3. Initialize a Repository
4. Add Individual File or All Files To Staging Area
5. Check a Repository Status
6. Commit Changes With a Single Line Message or Through an Editor
7. View Commit History With Changes
8. View a Particular Commit
9. View Changes Before Committing
10. Remove Tracked Files From The Current Working Tree
11. Rename Files
12. Revert Unstaged and Staged Changes
13. Amend The Most Recent Commit
14. Rollback Last Commit
15. Rollback a Particular Commit
16. Create and Switch To a New Branch
17. List All Branches
18. Delete a Branch
19. Merge Two Branches
20. Show Commit Log as Graph For Current or All Branches
21. Abort a Conflicting Merge
22. Add a Remote Repository
23. View Remote URLs
24. Get Additional Information About a Remote Repository
25. Push Changes To a Remote Repository
26. Pull Changes From a Remote Repository
27. Merge Remote Repository With Local Repository
28. Push a New Branch To Remote Repository
29. Remove a Remote Branch
30. Use Rebase

# 1. Set Up Your Username and Email

The username is required to link commits with your name. It is not the same as your GitHub account username, which you use to login into your GitHub profile. You can set or update your username by using the `git config` command. The new name will automatically reflect in any future commits that you push to GitHub from the command line. If you want to hide your real name, you can use any arbitrary text as your Git username.

```
git config --global user.name "<Your Name>"
```

You can also use the `git config` command to update the email address that you want to associate with your Git commits. The new email address will automatically reflect in any future commits that you push to GitHub from the command line.

```
git config --global user.email "<Your email>"
```

# 2. Cache Your Login Credentials

You can cache your login credentials by using the `config` parameter and `--global` flag. It helps to avoid re-typing the username and password every time you perform a commit.

```
git config --global credential.helper cache
```

# 3. Initialize a Repository

You can create an empty Git repository or reinitialize an existing one by using the `init` parameter. It will create a hidden directory upon initialization. This directory contains all the objects and references that Git uses and creates as a part of your project’s history.

```
git init
```

# 4. Add Individual Files or All Files To Staging Area

You can add a single file to the staging area by using the `add` parameter and the name of the file. Just replace the `somefile.js` with your filename.

```
git add somefile.js
```

You can also add all files and directories to the staging area y providing the wildcard instead of the file name.

```
git add .
```

# 5. Check a Repository Status

You can view the status of the current repository by using the `status` keyword, which includes the staged, unstaged, and untracked files.

```
git status
```

# 6. Commit Changes With a Single Line Message or Through an Editor

You can add a single-line message while making a commit in your repository by using the `commit` parameter, and `-m` flag. This message should immediately follow the flag and be wrapped in quotation marks.

```
git commit -m "Your short summary about the commit"
```

You can also open a text editor in the terminal to write a complete commit message. This message can contain multi-line text to allow you to explain the changes made to a repository in a detailed way.

```
git commit
```

# 7. View Commit History With Changes

You can view the changes made in your repository by using the `log` parameter. It will show a list of the newest commits in sequential order. You can also check the detailed changes of each file by adding the `-p` flag.

```
git log -p
```

# 8. View a Particular Commit

You can see the detailed changes of a specific commit by using the `show` parameter and providing the ID or hash of the commit. This hash is unique for each commit made in your repository.

```
git show 1af17e73721dbe0c40011b82ed4bb1a7dbe3ce29
```

You can also provide a short hash to get the same result.

```
git show 1af17e
```

# 9. View Changes Before Committing

You can view the list of changes made to your repository by using the `diff` parameter. It will only show the unstaged changes by default.

```
git diff
```

If you want to view the staged changes, you can add the `--staged` flag.

```
git diff --staged
```

You can also provide a filename as a parameter to only view the changes of a specific file.

```
git diff somefile.js
```

# 10. Remove Tracked Files From The Current Working Tree

You can remove files from the current working tree by using the `rm` parameter. This action will also remove the files from the index.

```
git rm dirname/somefile.js
```

You can also provide file globs (e.g., *.js) to remove all matching files.

```
git rm dirname/*.html
```

# 11. Rename Files

You can rename a file or directory by using the `mv` parameter. This parameter requires a `<source>` and a `<destination>`. The source must exist and can be a file, or directory, and the destination must be an existing directory.

```
git mv dir1/somefile.js dir2
```

Executing the above command will move the source(s) into the target directory. The index will get updated, but you have to commit the changes.

# 12. Revert Unstaged and Staged Changes

You can restore the unstaged working tree files by using the `checkout` parameter. You need to provide a file path to update it. If the file path is not set, then `git checkout` will update the HEAD to set the specified branch as the current branch.

```
git checkout somefile.js
```

To restore a staged working tree file, you can use the `reset` parameter. You need to provide a file path to remove it from the staging area. This will not remove any changes or modifications done to the files, instead, the file will be considered as an unstaged file.

```
git reset HEAD somefile.js
```

If you want to unstage all staged files, then do not provide the file path.

```
git reset HEAD
```

# 13. Amend The Most Recent Commit

You can make changes to the most recent commit by using the `commit` parameter with the `--amend` flag. For instance, you just committed some files, and you remember that you have made a mistake in your commit message. In such a scenario, you can execute this command to edit the previous commit’s message without modifying its snapshot.

```
git commit --amend -m "Updated message for the previous commit"
```

It is also possible to make changes to the previously committed files. For instance, you have updated some files in multiple folders that you want to commit in a single snapshot, but then you forgot to add one folder to the commit. Fixing this sort of error is just a matter of staging the other files or folders, and committing with the `--amend` and `--no-edit` flags.

```
git add dir1
git commit# Here you forgot to add dir2 to commit, you can execute the following command to amend the other files and folders.git add dir2
git commit --amend --no-edit
```

The `--no-edit` flag will allow you to correct your commit without altering its commit message. The final commit will then replace the incomplete one, and it will look like we have committed the changes to all updated files and folders in one snapshot.

> **Alert !!! Don’t amend public commits.
> **Correcting a local commit with amend is excellent, and you are allowed to push it to a shared repository. But you should avoid amending commits that are already public. Remember that the amended commits are completely new commits, and the previous commit will not be available on your current branch. It has the same consequence as resetting a public snapshot.

# 14. Rollback Last Commit

You can roll back the last commit by using the `revert` parameter. This will create a new commit, and revert the command previous commit, and add it to the current branch history.

```
git revert HEAD
```

**Revert v/s Reset**

The `git revert`command only undoes a single commit. It does not move back to the previous state of a project by removing all succeeding commits, which is done when `git reset` is used.

Reverting has two major benefits over resetting. First, it doesn’t alter the project history, which makes it a safe operation backward. Second, it can target a specific commit at any point in history, whereas git reset can only work backward from the current commit. For instance, if you want to undo an old commit with git reset, you would have to remove all the commits that occurred after the target commit, then re-commit all the subsequent commits. Thus, the `git revert` is a much better and safer way to undo the changes.

# 15. Rollback a Particular Commit

You can roll back to a particular commit by using the `revert` parameter and the commit ID. It will create a new commit, a copy of the provided commit ID, and add it to the current branch history.

```
git revert 1af17e
```

# 16. Create and Switch To a New Branch

You can create a new branch by using the `branch` parameter and the name of the branch.

```
git branch new_branch_name
```

But Git won’t switch to it automatically. If you want Git to auto-switch, you have to pass the `-b` flag and the `checkout` parameter.

```
git checkout -b new_branch_name
```

# 17. List All Branches

You can view the list of all branches by using the `branch` parameter. It will display all branches and mark the current branch with an asterisk (*) sign and highlight it.

```
git branch
```

You can also list all remote branches by using the `-a` flag.

```
git branch -a
```

# 18. Delete a Branch

You can delete a branch by using the `branch` parameter, the `-d` flag, and the name of the branch. If you’ve completed working on a branch and have merged it into the main branch, you can delete the branch without losing any history. However, if the branch hasn’t been merged, the delete command will output an error message. This safeguards you from losing access to your files.

```
git branch -d existing_branch_name
```

If you want to forcibly delete a branch, you can use the capital `-D` flag. This will delete the branch despite its current status and without any warning.

```
git branch -D existing_branch_name
```

The above commands will only delete a local copy of the branch. The branch may exist in the remote repository. If you want to delete a remote branch, then execute the following command.

```
git push origin --delete existing_branch_name
```

# 19. Merge Two Branches

You can merge two branches by using the `merge` parameter and the name of the branch. This will combine the specified branch into the main branch.

```
git merge existing_branch_name
```

If you need a merge commit, you can execute git merge with the `--no-ff` flag.

```
git merge --no-ff existing_branch_name
```

The above command will merge the specified branch into the main branch and generate a merge commit. This is essential to document all merges that occur in your repository.

# 20. Show Commit Log as Graph For Current or All Branches

You can view the commit log as a graph for the current branch by using the `log` parameter and `--graph --oneline --decorate` flags. The `--graph` option will draw an ASCII graph, which represents the branch structure of the commit history. When it is used in association with the `--oneline` and `--decorate` flags, it makes it easier to identify which commit belongs to which branch.

```
git log --graph --oneline --decorate
```

If you want to see the commit log for all branches, you can use the `--all` flag.

```
git log --all --graph --oneline --decorate
```

# 21. Abort a Conflicting Merge

You can abort a conflicting merge by using the `merge` parameter and the `--abort` flag. It allows you to exit from the merge process and return to the state after which the merge began.

```
git merge --abort
```

You can also use the `reset` parameter ...during a merge conflict to reset the conflicted files to a stable state.

```
git reset
```

# 22. Add a Remote Repository

You can add the parameters repository by using the `remote add parameter, `<shortname>, ` and the `<url>` awesomeapp repository.

```
git remote add awesomeapp https://github.com/someurl..
```

# 23. View Remote URLs

You can view the remote  URLs by using the `remote` parameter and the `-v` flag. This will list the remote connections you have to other repositories.

```
git remote -v
```

The above command is an interface to manage a list of remote entries that are stored in the repository’s `.git/config` file.

# 24. Get Additional Information About a Remote Repository

You can get detailed information about a remote repository by using the `remote-like parameter. and the name of the remote like `origin`.

```
git remote show origin
```

The above command will output a list of branches that are associated with the remote and also the endpoints that are connected to fetch and push files.

# 25. Push Changes To a Remote Repository

You can push changes to a remote the repository's name, the branch's name repository, and the name of the branch.

```
git push origin main
```

The above command will help you to upload the local changes to a central repository so that other team members can view the changes you have made.

# 26. Pull Changes From a Remote Repository

You can pull changes from a remote repository by using the `pull` parameter. This will fetch the specified remote’s copy of the current branch and instantly merge it into the local copy.

```
git pull
```

You can also view the details of the files that have been downloaded, by using the `--verbose` flag.

```
git pull --verbose
```

# 27. Merge the Remote Repository With the Local Repository

You can merge a remote repository with your local repository by using the `merge` parameter and the name of the remote.

```
git merge origin
```

# 28. Push a New Branch To Remote Repository

You can push a new branch to a remote repository bremote's name, the branch's name the remote, and the name of the branch.

```
git push -u origin new_branch
```

# 29. Remove a Remote Branch

You can remove a remote branch by using the `push` parameter, `--delete` flag, the name of the remote, and the name of the branch.

```
git push --delete origin existing_branch
```

# 30. Use Rebase

You can use this feature by using the `rebase` parameter and the name of the branch. Rebasing is a process to combine or move a sequence of commits to a new base commit.

```
git rebase branch_name
```

The above command will change the base of your branch from one commit to another, which will make it appear as if you have created your branch from a different commit. Git creates new commits and applies them to the specified base. It’s very necessary to understand that even though the branch looks the same, it’s comprised of entirely new commits.

Kudos! You have completed learning the top 30 commands offered by the Git CLI. Keep practicing the above-listed commands and you will be a master in managing your GitHub repositories.

> If you enjoyed reading this post and have learned something new, then please give a clap, share it with your friends, and follow me to get updates for my upcoming posts. You can connect with me on [LinkedIn](https://www.linkedin.com/in/kyriacos-antoniades).