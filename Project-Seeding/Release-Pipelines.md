# What is a CI?
CI stands for Continuous Integration. This allows the core team to integrate (and build) their code seamlessly while also maintaining code quality using Gated Check-in. That is where static analysis tools, tests, and build are ran

# What is a CD?
CD stands for Continuous Delivery. This provisions deployed environments like dev-staging-prod to be continuously updated when the codebase is updated

*Note that for operation critical environments like prod should require Approvals before deployment


---

For Project Seeding, we will only need to setup the CI/CD for one environment or the `dev`. The project lead or anyone that is taking over the project eventually is expected to setup the next environment (most of the time `staging`) so that the whole CI/CD management knowledge is turned over.


# What CI builds are needed?

## Gated Check-in
The Gated Check-in is a CI/build that runs whenever someone attempts to push their code changes to the repository. This build is expected to run a few things such as build, and static analysis tools such as `StyleCop` or `TSLint`. When this build fails, the code is not allowed to be merged. This prevent developers from pushing sub-standard or non-working code to our repository.
