# Setup `git nuke`

This repo exists so I can quickly restore my custom `git nuke` command on any new machine.

## What it does

`git nuke <branch>` deletes:

- the local branch
- the matching remote branch on `origin`

It also:

- requires an explicit branch name
- refuses to delete the currently checked out branch
- prints a message instead of trying to delete the active branch
- refuses to delete protected branches like `main`, `master`, or `develop`

## 1. Clone this repo

```bash
git clone https://github.com/<your-username>/<your-repo>.git ~/git-nuke
```

## 2. Make the script executable
```bash
chmod +x ~/git-nuke/git-nuke
```

## 3. Register the Git alias
```bash
git config --global alias.nuke '!~/git-nuke/git-nuke'
```

## 4. Use it
```bash
git nuke feature/my-branch
```

## Remove it later if you want
```bash
git config --global --unset alias.nuke && rm -rf ~/git-nuke
```
