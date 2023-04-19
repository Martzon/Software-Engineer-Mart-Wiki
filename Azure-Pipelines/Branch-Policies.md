## Branch Policies
After getting familiar with branching strategies, the next step on building proper environment branches is setting up branch policies.

Branch policies are an important part of the Git workflow and enable you to:

- Isolate work in progress from the completed work in your master branch
- Guarantee changes build before they get to master
- Limit who can contribute to specific branches
- Enforce who can create branches and the naming guidelines for the branches
- Automatically include the right reviewers for every code change
- Enforce best practices with required code reviewers

Branch policies limit direct code changes into a branch by requiring pull requests (PR) to be submitted. This is where we set the necessary gated check-in pipeline, which would be discussed below.
