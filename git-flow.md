# LUSH Digital Git Workflow For Android Projects
All Android projects use the git-flow workflow, which is breifly explained here:
https://www.atlassian.com/git/tutorials/comparing-workflows#gitflow-workflow
(Apologies for the Atlassian link)

All merges into branches must be merge commits.

To explain in the context of LUSH Digital, this is what each branch is used for:

## develop
All currently completed features, regardless of QA state. It's basically everything that's been developed for the project and reaches master via release branch. This is the branch that a QA analyst will assess from.

## master
Reflects exactly what is currently in production. It's likely that the project will CI and CD so master will automatically deploy again upon changes to the branch. All changes on this branch need to be tagged against the release they correspond to in production.

## feature/feature-name
Each feature in the backlog for any project will become it's own branch in git. All commits towards creating this feature will go onto this branch, then upon completing the feature, create a merge commit for this branch and merge it onto develop where it will then be tested. Feature branch names are hyphen-separated.

## release/vx.x
The intermediary step between develop and master. Branch from develop and this branch then becomes the branch that gets tested; Once it's believed that this snapshot of the project is stable, it is then merged in master and tagged with the version code. It is also then merged into develop if there were fixes made.
