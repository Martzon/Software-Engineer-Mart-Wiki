A project will usually have 3 branches that also correspond to 3 deployed environments and topic branches that developers could work on locally for their work items or feature/s they are currently working on. The environment branches are **dev**, **staging**, and **production**. A branching strategy is executed together with the version control system (git). Below are useful explanations why we need branches and why we need at least three of them

---

## Topic/Feature Branch
This branch serves as the developer’s working branch in which all WIP (work-in-progress) commits can be pushed. This branch will then be merged into **dev** by submitting a pull request, which can then be reviewed by other developers. 

Standard naming conventions:
- feature/<name-of-feature>
- <username>/<sprintNo or bugfix or hotfix>/<name-of-topic>


## Dev Branch/Environment
The dev branch is where the developers can push their changes once the development is done, as the name suggests. This enables the team to test changes as early as possible and potentially fix bugs for a more stable release. The dev branch is the default branch, that means all work should be done in dev almost always, followed by staging, and lastly prod (or master).

What changes need to go to the dev branch?
- Sprint items such as user stories and features
- Bug items included in the sprint
  - Or non-urgent, low priority bug items 

## Staging Branch/Environment
This branch serves as the testing ground for project managers/product owners to check on new features that are to be deployed to production. A corresponding app is deployed with this branch’s code. In some instances, this environment is also used by the client themselves for user-acceptance testing (if a separate UAT environment isn’t set up). The code in this branch should always be based on the code from the **production** environment and will only deviate when new code from **dev** comes in for an impending deployment.

## Production Branch/Environment
The branch that holds the code for the production site. This is also named **master** by default when creating new repositories.
