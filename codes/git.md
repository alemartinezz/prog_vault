# Git

## 🌲 Branches

Current branch

```shell
$(git branch --show-current)
```

Ver branches en orden de last committed

```shell
git branch --sort=-committerdate
```

Show all branches sorted by date of updation

```shell
git fetch && git for-each-ref --sort=-committerdate refs/heads/ refs/remotes/ --format='%(committerdate:short) %(refname:short)'
```

Delete all local branches which are not in remote

```shell
git fetch -p && git branch -vv | grep 'origin/.*: gone]' | awk '{print $1}' | xargs git branch -D
```

## 🔨 Utils

See latest commits in graph mode

```shell
git log --all --decorate --oneline --graph
```

Hard pull

```shell
git fetch --all && git reset --hard origin/dev
```

Resolve branch conflicts

```shell
git checkout dev && git pull && git checkout - && git rebase dev
```

```shell
git rebase --continue
```

```shell
git add . && git commit -m $(git branch --show-current) && git push -f origin $(git branch --show-current)
```

## 👹 From local folder to GitHub repo

```shell
mkdir -p <project> && cd <project>
```

```shell
git init
```

```shell
git remote add origin git@github.com:alemartinezz/course-python-3-programming.git
```

Optional, if repo already initialized:

```shell
git fetch --all && git pull origin main --allow-unrelated-histories
```

Continue:

```shell
git branch -M main && git add . && git commit -m "initial commit" && git push -u origin main
```

## ⏬ Integrate dev updates into current branch

Update local dev branch

```shell
git stash && git checkout dev && git fetch --all && git pull && git checkout <branch_name>
```

Rebase dev branch into yours

```shell
git rebase dev && git stash apply
```

Verify

```shell
git log
```

Upload

```shell
git add . && git commit -m "Commit message" && git push origin <branch_name>
```
