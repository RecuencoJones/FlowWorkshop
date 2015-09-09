# FlowWorkshop

## Prerequisites:

`Git` installed
Contributor rights on remote repository (GitHub, GitLab, BitBucket, Stash, ...)

## Suggestions:

You can always let a UI-client do the job, but we prefer working straight with the console so we have a better control and knowledge over git commands.

We recommend using **git bash** console when working with git because:

- It standarizes all paths (/this/is/how/paths/work) and commands (ls, cp, mv, rm) to UNIX.
- It will suggest arguments for our commands using TAB key.
- Finally, it won't interfere with our basic CMD.

## Git configuration

### Username and email

To set your username and email, which will be set whenever you commit in order to identify you as author of that commit you have to write these commands:

`git config --global user.name "Doe, John"`
`git config --global user.email john.doe@foo-bar.com`

There are several more commands that you can configure, check [git-config](http://git-scm.com/docs/git-config) reference for more info.

### Cloning a project into local

In order to clone a project, we will check for the **clone** button which will highlight a URL we have to copy, then in the console:

`git clone URL`

The project will be cloned into a new folder with the name of the project, so we have to move into that folder.

`cd PROJECTFOLDER`

We will find some .git* files inside the project, these are project level settings. Most common files are:

- [.gitignore](http://git-scm.com/docs/gitignore): this file contains name patterns that will be ignored from VCS and therefore won't be tracked nor pushed by git.
- [.gitattributes](http://git-scm.com/docs/gitattributes): this file contains settings for files to be treated in a special way if necessary. For example, to treat images as binaries and therefore don't track them for internal changes, to set line endings as CRLF or LF, etc.
- [.gitmodules](http://git-scm.com/docs/gitmodules): this file is weird to find, but it's used to import repositories into other repos.
- [.gitconfig](http://git-scm.com/docs/gitconfig): this gile includes local git configurations, like using https:// instead of git://

Also, most repositories include a README.md file like this to explain repository contents.

### Commit, push and pull

These three are the most important commands in git.

#### Commit

Commits are the basic unit of VCS, it represent a frozen step in the past which contains all the changes made until that point and therefore, the list of commits represent a history of the repository changes. Whenever some changes on the code are done and to save its state we will commit, but first we have to add the files to the commit state.

In order to do this:

`git add files/to/be/committed` or shorter, add all files to commit `git add -A`

and then

`git commit -m "FEATURECODE VERB description"`

this is the short way to commit, for example:

`git commit -m "CMP-33 UPDATE modified some file"`

You can also type `git commit` and VIM editor will open so you can write commit header and body.

All commits we do will be saved in our local repository and we will have to push them to the remote branch.

#### Push

With this command we send our local committed changes to the remote repository from where we cloned. The way to push is like this:

`git push REMOTE BRANCH`

most of the time REMOTE will be origin and BRANCH the branch you're currently working on (NEVER EVER PUSH TO MASTER OR DEVELOP). For example:

`git push origin feature/CMP-33`

After introducing our password, the commits will be sent to the remote and appended to the HEAD of the branch.

#### Pull

In order to get changes that were made in the remote repository, we need to bring them to our branches. Most commonly, develop branch will be updated after some pull request and we will have to bring those changes in order to be up to date. So we type:

`git pull REMOTE BRANCH`

in this case:

`git pull origin develop`

and the commits from that branch will be merged with our current working branch.
Most of the times this shouldn't be conflictive.

#### Other commands

We can check which files are modified, created or deleted with `git status`, also, `git add` and `git rm` will add or remove files to the commit and therefore from the repository. `git merge` is a rarely used command to merge branches locally. `git diff` provides us with a complete output with differences between tracked and modified files.

### Working with branches

In order to track remote branches and swap amongst them, we have some more commands:

`git fetch` will check for remote repository status, and if there are new branches, it will automatically create local branches set up to track those. Also it will give us info on how many commits we're ahead or behind other branches.

`git branch` will output what is our currently working branch

`git checkout BRANCHNAME` will change the currently working branch to the one we specify. Also, if we want to change branches undoing all changes we did in the other branch we can use `git checkout BRANCHNAME --force` of we can **stash** the changes so we can apply them later again, this is done with `git stash`, read more in the docs: [git-stash](http://git-scm.com/docs/git-stash)

### Git flow

Git flow is the process of working with git. This process follows some steps:

1. Clone repository.
2. Create issue branch (manually, via Jira, etc).
3. Fetch repository changes.
4. Pull changes from base branch (develop).
5. Code.
6. Add and commit the changes locally.
7. Push commits to remote branch.
8. Create a pull request from the web app, be it Stash, GitHub, BitBucket, etc.
9. Repeat from 2.
