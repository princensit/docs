# Git Branching Strategy

Create a feature branch from master where the feature is ready to be tested. Naming practice could be: dev_<jiraid>_<info about feature branch if needed>
Ex- dev_TASK-111_user_creation

After the feature has been tested in feature branch, create a new release branch from master by bumping the version number. Make sure to open a pull request against master before actually deploying the branch into production.

A git branch naming practice that we could follow is as: release_<version_number>
release_1.0.0
(Major) (Minor) (Patch)

Once this release branch goes live in production, merge it back into master. Master is always a updated branch.

In case of some hotfixes on this release branch, always opens a pull request against master and bump the patch version number and deploy to production, and merge back into master.

CMR: Make sure to fill the essential details specially rollback plan while creating the CMR.

Reference: https://nvie.com/posts/a-successful-git-branching-model/
