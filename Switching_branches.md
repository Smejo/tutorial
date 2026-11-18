# Switching to Another Branch (VS Code)

## 1. Switch the branch

- Click the branch name in the bottom-left corner of VS Code and pick the branch.
  Or press `Ctrl+Shift+P` → **Git: Checkout to...** → pick the branch.
- Older branches that exist only on GitHub: run **Git: Fetch** first (`Ctrl+Shift+P`), then they appear in the list.

Terminal equivalent:

```bash
git checkout branchName
```

## 2. Check the state

```bash
git status
```

You should see `On branch branchName` and `nothing to commit, working tree clean`.

## 3. Make your local copy identical to GitHub (optional)

If the branch is outdated or messy locally and you want exactly what is on GitHub:

```bash
git fetch
git reset --hard origin/branchName
```

> ⚠️ **Warning:** `git reset --hard` permanently deletes all uncommitted changes and any commits that were not pushed to GitHub. Make sure you have nothing there you want to keep.

## If checkout is refused

`Your local changes would be overwritten` means you have uncommitted changes. Commit them in the Source Control panel first (or discard them if you don't need them).
