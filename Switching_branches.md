# Switching Between Branches (Including Older Ones)

A step-by-step guide to moving between branches in Git, with a focus on getting to older branches and older states of the project.

## 1. Check where you are and save your work

1. Open a terminal in the project folder (in VS Code: **Terminal → New Terminal**).
2. Check the current branch and any uncommitted changes:

   ```bash
   git status
   ```

3. If you have uncommitted changes, either commit them or stash them (see [Troubleshooting](#troubleshooting)):

   ```bash
   git add .
   git commit -m "Describe your changes"
   ```

## 2. Update the list of branches from GitHub

Older branches may exist on GitHub but not yet on your computer. Fetch them:

```bash
git fetch --all
```

## 3. List the available branches

```bash
git branch        # local branches only
git branch -a     # local + remote branches
```

Remote branches appear as `remotes/origin/<name>`. The current branch is marked with `*`.

## 4. Switch to a branch

### A branch that exists locally

```bash
git switch <branch-name>
```

Example: `git switch main`

### An older branch that exists only on GitHub (remote)

```bash
git switch <branch-name>
```

If `origin/<branch-name>` exists, Git automatically creates a local branch that tracks it. If that doesn't work, be explicit:

```bash
git switch -c <branch-name> origin/<branch-name>
```

Example: `git switch -c add-github-tutorial origin/add-github-tutorial`

> `git checkout <branch-name>` does the same thing. `git switch` is the newer, clearer command.

### In VS Code

1. Click the branch name in the bottom-left corner of the window (status bar).
2. Pick the branch from the list. Remote branches are shown with `origin/`.

## 5. Verify the switch

```bash
git status
git log --oneline -5
```

The first line of `git status` shows `On branch <branch-name>`. The files in your folder now match that branch.

## 6. Go back to an older state (commit or tag)

To look at the project as it was at a specific point in time:

1. Find the commit or tag:

   ```bash
   git log --oneline
   git tag
   ```

2. Check it out:

   ```bash
   git switch --detach <commit-hash-or-tag>
   ```

   Example: `git switch --detach 735e1c8`

This puts you in a **detached HEAD** state: you can look around and run things, but commits you make here do not belong to any branch.

### To keep working from that old point

Create a new branch from it:

```bash
git switch -c my-new-branch
```

### To leave the old state

```bash
git switch main
```

## 7. Switch back to the previous branch

```bash
git switch -
```

## Troubleshooting

| Problem | Solution |
| --- | --- |
| `error: Your local changes would be overwritten by checkout` | Commit your changes, or stash them: `git stash`, switch branches, then restore with `git stash pop`. |
| `fatal: invalid reference: <name>` | The branch is not known locally. Run `git fetch --all` and check the name with `git branch -a`. |
| Branch seems to be missing | It may have been deleted on GitHub. Run `git fetch --all --prune` and check `git branch -a` again. |
| You are in "detached HEAD" and want to leave | Run `git switch main` (or any branch). To keep the work, first run `git switch -c <new-branch>`. |
| Files look outdated after switching | Run `git pull` to get the latest changes of that branch. |

## Quick cheat sheet

```bash
git fetch --all                   # get the latest branch list
git branch -a                     # list all branches
git switch <branch>               # switch to a branch
git switch -c <branch> origin/<branch>   # switch to a remote-only branch
git switch --detach <commit|tag>  # view an older commit or tag
git switch -                      # go back to the previous branch
git stash / git stash pop         # temporarily set aside changes
```
