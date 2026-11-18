# Switching to Another Branch (VS Code)

## 1. See which branches exist

- In VS Code: click the branch name in the bottom-left corner. The list shows local and remote branches.
- In the terminal:

```bash
git branch        # local branches (the current one is marked with *)
git branch -a     # local + remote branches (remotes start with remotes/origin/)
```

If a branch is missing, run **Git: Fetch** (`Ctrl+Shift+P`) or `git fetch` to download the latest branch list from GitHub.

## 2. Switch the branch

- Click the branch name in the bottom-left corner of VS Code and pick the branch.
  Or press `Ctrl+Shift+P` → **Git: Checkout to...** → pick the branch.
- Older branches that exist only on GitHub: fetch first (see step 1), then they appear in the list.

Terminal:

```bash
git switch branchName
```

### `git switch` vs `git checkout`

`git checkout` is the older command and does many unrelated things (switch branches, restore files, open old commits). `git switch` was added in Git 2.23 to do only one thing: switch branches. Both work the same for this guide, but `git switch` is clearer and harder to misuse.

| Task | Command |
| --- | --- |
| Switch to a branch | `git switch branchName` |
| Go back to the previous branch | `git switch -` |

If `git switch` says the command doesn't exist, your Git is older than 2.23. Use `git checkout branchName` or update Git.

## 3. Check the state

```bash
git status
```

You should see `On branch branchName` and `nothing to commit, working tree clean`.

## 4. Update the branch from GitHub (optional)

If your local branch is older than GitHub, first try a normal pull. It keeps your local work.

In VS Code: Source Control panel → `...` menu → **Pull** (or `Ctrl+Shift+P` → **Git: Pull**).

Terminal:

```bash
git pull
```

### If the pull fails or the branch has diverged

A pull can fail with `Your local changes would be overwritten`, `Not possible to fast-forward`, or merge conflicts. This happens when your local branch has commits (or uncommitted changes) that GitHub doesn't have, and GitHub has commits you don't have (the branches have "diverged").

Choose one:

- **Keep your local work:** commit or stash your changes (see below), then `git pull` again and resolve any merge conflicts.
- **Throw away your local work and match GitHub exactly:** use the hard reset below.

```bash
git fetch
git reset --hard origin/branchName
```

> ⚠️ **Warning:** `git reset --hard` permanently deletes all uncommitted changes and any commits that were not pushed to GitHub. Make sure you have nothing there you want to keep.

VS Code has no button for a hard reset, so run it in the integrated terminal (``Ctrl+` ``).

### Switch and match GitHub in one command

```bash
git fetch origin && git switch -C branchName origin/branchName --discard-changes
```

`-C` creates the branch or resets it to `origin/branchName`, and `--discard-changes` also drops uncommitted changes. The same warning applies.

## If checkout is refused

`Your local changes would be overwritten` means you have uncommitted changes. You have three options:

- **Commit** them in the Source Control panel.
- **Discard** them if you don't need them.
- **Stash** them if you aren't ready to commit but want to keep them (see below).

### Stash: park your changes temporarily

Stashing saves your uncommitted changes aside and gives you a clean working tree, so you can switch branches.

In VS Code: Source Control panel → `...` menu → **Stash** → **Stash** (or **Stash (Include Untracked)** to also include new files). Switch branches and do what you need. To get your changes back: `...` menu → **Stash** → **Pop Latest Stash**.

Terminal:

```bash
git stash                  # save changes and clean the working tree
git switch otherBranch     # do what you need on the other branch
git switch originalBranch  # come back
git stash pop              # restore your changes
```

Notes:

- New (untracked) files are not stashed by default. Use `git stash -u` to include them.
- A stash belongs to the repository, not to a branch. You can pop it on a different branch than the one you stashed on, so pop it where you intend to.
- `git stash list` shows all saved stashes.
- If `git stash pop` reports a conflict, resolve it like a merge conflict. The stash is kept until the pop succeeds.
