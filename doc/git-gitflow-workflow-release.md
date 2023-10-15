# Git: Gitflow Workflow - Release

```sh
# create release/0.1.0 branch from develop branch
git checkout develop
git pull
git checkout -b release/0.1.0
git push -u origin release/0.1.0

# create FIX-001/fix_001 branch from release/0.1.0 branch
# IMPORTANT: no new features allowed, only fixes, docs and other release related work
git checkout release/0.1.0
git pull
git checkout -b FIX-001/fix_001

# work happens on FIX-001/fix_001 branch
git add --all && git commit -m 'feat: FIX-001/fix_001'
git push -u origin FIX-001/fix_001
# pull request happens on FIX-001/fix_001 branch

# merge release/0.1.0 branch to FIX-001/fix_001 branch
git checkout release/0.1.0
git pull
git checkout FIX-001/fix_001
git merge release/0.1.0
# code merge conflicts happens on FIX-001/fix_001
git add --all && git commit -m 'chore: merge release/0.1.0 to FIX-001/fix_001'
git push

# merge FIX-001/fix_001 branch to release/0.1.0 branch and delete FIX-001/fix_001 branch
git checkout release/0.1.0
git pull
git merge FIX-001/fix_001
git push
git branch -D FIX-001/fix_001

# update release version in package.json and changelog.md files with a custom 'make:changelog' script
npm version 0.1.0
npm run make:barrel # optional: make barrels automatically
npm run make:changelog
npm shrinkwrap # optional: only when producing production packages to be deployed on a server
git add --all && git commit -m 'chore(release): barrels, changelog'
git push && git push --tags

# OPTIONAL: list all tags, assign a new tag with the release data in main branch
# this step is optional as 'npm version 0.1.0' command also creates a 'v0.1.0' tag
git tag -l -n3
git tag -a v0.1.0 -m "chore(release): Release v0.1.0"
git push --tags

# merge release/0.1.0 branch to develop branch
git checkout develop
git pull
git merge release/0.1.0
# code merge conflicts happens on develop branch
git add --all && git commit -m 'chore: merge release/0.1.0 to develop'
git push

# merge release/0.1.0 branch to main branch
git checkout main
git pull
git merge release/0.1.0
# code merge conflicts happens on develop branch
git add --all && git commit -m 'chore: merge release/0.1.0 to main'
git push

# checkout to develop branch
git checkout develop
git pull
```
