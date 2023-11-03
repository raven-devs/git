# Git

## Commamds

```bash
# config
git config --get remote.origin.url
git config --local --list
git config --local user.name $user_name
git config --local user.email $user_email

# clone a repo
git clone $repo_url $dir

# show remote
git remote
git remote show origin
git ls-remote $repo_url

# list all branches local / remote
git branch
git branch -r

# delete a branch local / remote
git branch -D $branch
git push origin --delete $branch

# checkout to a new branch from a current one, commit changes and push
git checkout -b $new_branch
git add --all
git commit -m $message
git push

# checkout to a previouse branch and pull the latest changes
git checkout -
git checkout $branch
git pull

# commit with a tag
git add -all
git commit -m $message
git tag -f v1.0
git push origin --tags

# merge a branch onto a current branch
git merge $branch

# unmodify
git checkout -- .
git checkout -- $file

# unstage
git reset --hard HEAD
git reset --hard HEAD $file

# cancel a previous local commit
git reset --hard HEAD~1

# cancel a last push to a branch
git push -f origin $last_ok_commit:$branch
git push -f origin 6f55ff2744b09872fa4fd8dfdb2f4c724d2c9916:develop

# unmerge
git reset --merge
git merge --abort

# force to overwrite local with remote
git fetch --all
git reset --hard origin/$branch_name

# force to overwrite remote with local
git push origin $branch --force

# overwrite a remote branch with a different local branch, use the local-name:remote-name syntax for git push
git push origin $new_branch:$old_branch -f

# display log and diff
git log
git log --pretty=oneline
git log --pretty=oneline --graph
git log --pretty=fulle
git log --stat --summary
git log --author=spetushkov --since="2023-01-01" --pretty=oneline
git log --author="spetushkov" --since="2023-01-01" --pretty=oneline | wc -l
git diff
git diff --staged

# fix a .gitignore cache issue
git rm -r --cached .
git add --all && git commit -m "fix: .gitignore cache issue"
reload IDE
```

## pull vs fetch

The difference between pull and fetch is: Fetch just downloads the objects and refs from a remote repository and normally updates the remote tracking branches. Pull, however, will not only download the changes, but also merges them - it is the combination of fetch and merge.
