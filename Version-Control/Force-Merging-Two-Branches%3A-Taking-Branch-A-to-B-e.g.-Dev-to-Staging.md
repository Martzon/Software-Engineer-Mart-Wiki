There will be times that you would want to merge `dev` to `staging` and you know that the `dev` branch is your source of truth and You just need to move all changes in `dev` to `staging`.

**Warning**: Before doing this, make sure that there weren't any commits pushed directly to `staging` that weren't `cherry-picked` back to `dev`. Otherwise, please `cherry-pick` or "merge down" those changes first back to `dev` from `staging`

**Warning #2**: If you are not sure if there have been unmerged commits, just proceed accordingly and expect **conflicts**. Resolve them carefully. You might introduce **broken features/bugs**

---
We will use `source` and `target` branches. `dev` being the source and `staging` being the target. So next time you can explain or do this using abstract branch names: `source` and `target`

`source = dev`
`target = staging`

1. Ensure that you have the latest version of your `source` branch by running `git checkout dev` followed by `git pull`
2. Ensure that you ALSO have the latest version of your `target` branch by running `git checkout staging` followed by `git pull`
3. You should be still in your `target` branch `staging`; Create a branch from. `git checkout -b apanaligan/Sprint69/DevToStagingMerge`. This branch will be "Pull Requested"-ed to your `target` branch `staging` once the merge is done.
4. Next, merge the code using `git merge -X theirs dev`. This will merge all your `dev` changes to your `target`, current branch `staging`. Should conflict occurs, `git` will "take dev" (theirs') changes because of the `-X` flag.
5. `git push`
6. Create a PR in `Az DevOps`; be sure to validate the changes made. Though there shouldn't be any issues since you are just taking the changes from `dev` to `staging`. There are just some instances that conflicts might occur because some commits were pushed directly to `staging` and not merged back to `dev`