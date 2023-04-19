## Start New Work by Branching from a Branch e.g. `dev`
To start and push new work. You need to create a branch from a branch, most of the time the dev branch. To do this:

`git checkout dev`
`git pull`
`git checkout -b Sprint1/CustomerInvitation`
When your work is done, you need to push your changes by:
`git add .`
`git commit -m “Your commit message e.g. talk about what you worked on”`
`git push --set-upstream origin Sprint1/CustomerInvitation`

Once done, you will be able to find your branch in Azure DevOps. From there you may create a new `Pull Request`

**The steps above will be your bread-and-butter in pushing changes/work from time to time.**


## Branch Naming Conventions

```
{{email}}/{{sprint}}/{{feature or bug}}
apanaligan/Sprint1/LoginPage
apanaligan/Sprint1/CleanupItems
apanaligan/Sprint1/LoginFormBug
```

## Resolving Conflicts
Sometimes, similar files get updated by other devs that are also affected by your pull request. To fix this you must
1. Ensure that you are on your local branch e.g. apanaligan/Sprint1/LoginPage
1. Get all recent branches from the remote (origin) by using git fetch origin
1. Rebase your local branch against the dev branch using git rebase origin/dev
1. Fix conflicts
1. Push

## What if I accidentally committed my changes to dev and not my local branch?
1. You can easily checkout it to a new branch using `git checkout -b {{branch_name}}`
1. Once you push your changes, the commit will linger in your local dev branch. To reset it you need to run `git reset --hard origin/dev`. **Please make sure that you no longer need these changes i.e. you have already submitted a PR**

## Command Reference
1. `git checkout dev` - Checkouts a specific branch, where dev is the branch name. Note that checkout doesn’t pull the latest changes but only sets your branch to dev in this case
1. `git pull` - Pulls all changes/commits on your current branch. 
1. `git branch -b Sprint1/Database` - Creates a new branch from your current branch. -b means “create new branch” and Sprint1/Database is your branch name
1. `git push` - Pushes your commits to your branch.
1. `git fetch origin` - Fetches all changes against the current repository. Use this to get updated on the branches 
1. `git add .` - adds all files to current commit
1. `git commit -m “Sample”` - commits currently staged files while “Sample” is the commit message
1. `git rebase origin/dev` - attempts to merge commits from dev into your local/current branch. This should be used to merge conflict handling if need be.
1. `git reset ...` - Reset `commits`; It can unstage your files (from `git add`) or ERASE your local copy. So please be careful when using it. I suggest to read the official docs when using this command
1. `git status` - Checks for modified files, current branch, and another branch-related status
