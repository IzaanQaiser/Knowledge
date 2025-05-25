## Common git Commands:
1. initialise local repository - `git init` will make a repository on your local machine.
2. connect remote repository - `git remote add origin <remote-url>` will associate `origin` with the `remote-url`.
2. git add command - `git add .` will add all changes in tracked folders that you have made since last stage.
3. git commit command - `git commit -m "message"` will commit all staged changes with the "message" as the description.
4. git push command - `git push` will push all comitted changes to your remote repository on whatever branch you're on.
5. git unstage command - `git reset HEAD <filename>` OR `git reset HEAD .` will unstage filename, OR will unstage everything.
6. delete Git repository (local) - `rm -rf .git` will remove all Git tracking from the local machine (at that path).

6. wth im supposed to do with conflicts
7. wth is rebasing


## Making a **NEW BRANCH**
1. Make a branch titled `branch-name` in your remote repository (makes the branch in the remote repository)
2. Run `git checkout -b drafting` in your local repository (makes the branch in the local repository)
3. Run `git push --set-upstream origin branch-name` (pushes the local branch to the remote origin, linkes local to remote)