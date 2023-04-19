Please consider the following scenarios when setting up the Code Repository for your `production` (`master` branch)


### Stable `staging` branch/environment
Stable means it's **up-to-date** and **tested**. If this is the case you may create your `master` branch based on you stable `staging` branch

### Unstable `staging` branch/environment
If `staging` is unstable, obviously it needs to become stable first by letting the QA test everything. Once stable, you may merge to `master`

### Outdated `staging` branch/environment
If your `staging` is outdated, `dev` needs to be merged first and it has to be **stable** before it gets merged to `master`


### `master` already exists but outdated/broken state
As stated above, `staging` takes priority, if in any case `master` already exists, a stable `staging` branch should be merged to `master`. Note that when you merge, all changes from `staging` should be copied to `master`. You may do so by using the `theirs` command in `git` (git checkout master; git merge -X theirs staging)