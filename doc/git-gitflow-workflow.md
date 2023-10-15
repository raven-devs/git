# Git: Gitflow Workflow

<https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow>

## Init

```sh
# init git, create main branch, create develop branch from main branch
rm -rf .git
echo "# create-be-template" >> README.md
git init
git config user.name spetushkou
git config user.email sergey.petushkou@gmail.com
git remote add origin git@github.com:raven-devs/create-be-template.git
git checkout -b main
git add --all && git commit -m 'chore: init'
git push -u origin main
git checkout -b develop
git push -u origin develop
```

## Feature | Fix

```sh
# create FEAT-001/feature_001 branch from develop branch
git checkout develop
git pull
git checkout -b FEAT-001/feature_001

# work happens on FEAT-001/feature_001 branch
git add --all && git commit -m 'feat: FEAT-001/feature_001'
git push -u origin FEAT-001/feature_001
# pull request happens on FEAT-001/feature_001 branch

# merge develop branch to FEAT-001/feature_001 branch
git checkout develop
git pull
git checkout FEAT-001/feature_001
git merge develop
# code merge conflicts happens on FEAT-001/feature_001 branch
git add --all && git commit -m 'chore: merge develop to FEAT-001/feature_001'
git push

# merge FEAT-001/feature_001 branch to develop branch and delete FEAT-001/feature_001 branch
git checkout develop
git pull
git merge FEAT-001/feature_001
git push
git branch -D FEAT-001/feature_001
```

## Hotfix

```sh
# create hotfix branch from main branch
git checkout main
git pull
git checkout -b hotfix

# work happens on hotfix branch
git add --all && git commit -m 'fix: hotfix'
git push -u origin hotfix
# pull request happens on hotfix branch

# merge hotfix branch to develop branch
git checkout develop
git pull
git merge hotfix
# code merge conflicts happens on develop branch
git add --all && git commit -m 'chore: merge hotfix to develop'
git push

# merge hotfix branch to main branch
git checkout main
git pull
git merge hotfix
# code merge conflicts happens on main branch
git add --all && git commit -m 'merge hotfix to main'
git push

# checkout to develop branch and delete hotfix branch
git checkout develop
git pull
git branch -D hotfix
```

## Fix the issue when changes to the .gitignore file has no effect

```sh
git rm -r --cached .
git add --all && git commit -m "fix: .gitignore"
reload IDE
```

## Useful commands

```sh
git clone git@github.com:raven-devs/create-be-template.git another-project-dir

git branch
git branch -D $branch

git remote show origin
git config --get remote.origin.url
git ls-remote git@github.com:raven-devs/create-be-template.git

git checkout -b $new_branch
git add --all
git commit -m 'feat: new feature'
git push

git checkout -
git checkout $branch
git pull

git merge $branch
```

## .gitignore cache issue fix

```bash
git rm -r --cached .
git add --all && git commit -m "fix: .gitignore cache issue"

reload IDE
```
