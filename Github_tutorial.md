# **GitHub workflow**

1. Vyclonovaný repozitár (**clone**) – stačí prvý krát na danom notebooku alebo keď niečo totálne zblbne v gite.
2. V softvéri, v ktorom pracuješ, treba mať repozitár otvorený.
3. Na nový feature, zmenu alebo tool treba vytvoriť nový **branch**, ideálne z **main**.
4. Prepnúť sa na svoju **branch** (**checkout**) a jednotlivé zmeny postupne **commit**ovať (lokálne) a **push**ovať (GitHub). Commitovať len podstatné súbory.
5. Keď je práca dokončená, treba vytvoriť **pull request** na **merge**nutie branche do **main** branche.
6. Poprosiť niekoho z tímu o **review** zmien, prípadne zapracovať požadované zmeny.
7. Po **approve** na pull requeste môžeš **merge**núť branchu do **main** cez web interface GitHubu. Treba skontrolovať, či sa **main** medzitým neposunul, a prípadne spraviť **rebase** svojej **branche** nad aktuálny **main**.
8. **Branch** sa tým **merge**ne do **main** a stačí vymazať lokálnu aj GitHub branchu (upratať po sebe).
9. Pokiaľ šlo o nejakú verziovanú vec, treba na aktuálny **merge commit** v **main** hodiť **tag** (napr. `IoBoard/v2.0.3`) a ten tag treba **push**núť.

---

# **GitHub workflow (English)**

1. **Clone** the repository – only needed the first time on a given laptop, or when something goes completely wrong in git.
2. The repository must be open in the software you are working in.
3. For a new feature, change or tool, create a new **branch**, ideally from **main**.
4. Switch to your **branch** (**checkout**), then **commit** individual changes step by step (locally) and **push** them (to GitHub). Commit only the relevant files.
5. When the work is finished, create a **pull request** to **merge** the branch into the **main** branch.
6. Ask someone from the team to **review** the changes, and incorporate any requested changes.
7. After the pull request is **approved**, you can **merge** the branch into **main** via the GitHub web interface. Check whether **main** has moved in the meantime, and if so, **rebase** your branch onto the current **main**.
8. The branch is thereby **merged** into **main**, and you just need to delete the local and GitHub branch (clean up after yourself).
9. If it was a versioned item, put a **tag** (e.g. `IoBoard/v2.0.3`) on the current **merge commit** in **main**, and **push** that tag.

---

# **Detailed steps with VS Code (English)**

Step-by-step guide to the branch → commit → pull request → merge → tag workflow, using the VS Code Git integration and the GitHub website.

> **Where each step happens:** 🖥️ = VS Code, 🌐 = GitHub website

| Placeholder        | Meaning                                 | Example                  |
| ------------------ | --------------------------------------- | ------------------------ |
| `main`             | Default (base) branch of the repository | `main`, `develop`        |
| `<feature-branch>` | Your working branch                     | `feature/add-login-page` |
| `<file>`           | File(s) you changed                     | `docs/README.md`         |
| `<commit-message>` | Short description of the change         | `Add login page`         |
| `<version>`        | Release version for the tag             | `v1.2.0`                 |

## 1. Create the branch 🖥️

1. Click the current branch name (`main`) in the bottom-left status bar.
2. Choose **+ Create new branch from...**
3. Select `main` as the base, then name the branch `<feature-branch>`. VS Code switches to the new branch automatically.

> **Tip:** Make sure `main` is up to date first (**Source Control → `...` → Pull**).

## 2. Commit 🖥️

1. Open **Source Control** (`Ctrl+Shift+G`).
2. Under **Changes**, hover over `<file>` and click **+** to stage only that file.
3. Type `<commit-message>` in the message field above the **Commit** button.
4. Click **Commit**.

## 3. Push 🖥️

Click **Publish Branch** in Source Control (or the cloud icon in the status bar). This pushes `<feature-branch>` to GitHub. Later pushes use **Sync Changes**.

## 4. Create the pull request 🌐

1. Open the repository on github.com. A yellow banner, *"`<feature-branch>` had recent pushes"*, appears with a **Compare & pull request** button. Click it.
   - If the banner isn't there: open the **Pull requests** tab → **New pull request**, set **base** to `main` and **compare** to `<feature-branch>`.
2. Check that the base branch is `main`.
3. Fill in the title and description, then click **Create pull request**.

## 5. Review 🌐 / 🖥️

1. 🌐 In the PR's right sidebar, click **Reviewers** and pick a teammate.
2. 🖥️ If they request changes, edit the file(s) in VS Code, then commit and push again. The PR updates automatically.

## 6. Merge 🌐 / 🖥️

1. 🌐 Wait for approval (and for any CI checks to pass).
2. If the PR says the branch is out of date, either:
   - 🌐 Click **Update branch**, **or**
   - 🖥️ Rebase in VS Code: open the Command Palette (`Ctrl+Shift+P`), run **Git: Rebase Branch...**, choose `origin/main`, then push. A rebase requires a **force push**, which VS Code asks you to confirm.
3. 🌐 Click **Merge pull request**, then **Confirm merge**.

## 7. Clean up 🌐 / 🖥️

1. 🌐 On the merged PR page, click **Delete branch**.
2. 🖥️ Click the branch name in the status bar and switch to `main`.
3. 🖥️ In Source Control, click **`...` → Pull** to get the merged changes.
4. 🖥️ Open the Command Palette (`Ctrl+Shift+P`), run **Git: Delete Branch...**, and select `<feature-branch>`.

## 8. Tag a release 🖥️ / 🌐

Tag the merged commit on `main` so the release can be referenced later. Use [semantic versioning](https://semver.org/) (`vMAJOR.MINOR.PATCH`, e.g. `v1.2.0`).

### Option A: in VS Code 🖥️

1. Make sure you are on `main` and it is up to date (**Source Control → `...` → Pull**).
2. Open the Command Palette (`Ctrl+Shift+P`) and run **Git: Create Tag**.
3. Enter the tag name `<version>`, then a short message (e.g. `Release <version>`) to create an annotated tag.
4. Push the tag: Command Palette → **Git: Push Tags**. (Tags are not pushed by a normal push or Sync.)
5. 🌐 Optional: on GitHub, open **Releases → Draft a new release**, pick `<version>` from **Choose a tag**, add release notes, and click **Publish release**.

### Option B: on the GitHub website 🌐

1. Open the repository and go to **Releases** (right sidebar) → **Draft a new release**.
2. Click **Choose a tag**, type `<version>`, and select **Create new tag: `<version>` on publish**.
3. Set **Target** to `main`.
4. Add a title and release notes (**Generate release notes** fills them from merged PRs).
5. Click **Publish release**.
6. 🖥️ In VS Code, run **Git: Fetch** (Command Palette) to pull the new tag locally.

### Fixing a wrong tag

1. 🖥️ Command Palette → **Git: Delete Tag**, then select the tag (deletes it locally).
2. 🌐 On GitHub, go to **Tags**, open the tag (or its release), and delete it there.
3. Create the correct tag again with Option A or B.

> **Warning:** Avoid moving or reusing a tag that others may already have pulled. Prefer creating a new version (e.g. `v1.2.1`).

## Quick reference (Git CLI equivalents)

```bash
git switch main && git pull                      # update main
git switch -c <feature-branch>                   # 1. create branch
git add <file>                                   # 2. stage
git commit -m "<commit-message>"                 # 2. commit
git push -u origin <feature-branch>              # 3. push
git fetch origin && git rebase origin/main       # 6. rebase (optional)
git push --force-with-lease                      # 6. push after rebase
git switch main && git pull                      # 7. update main
git branch -d <feature-branch>                   # 7. delete local branch
git tag -a <version> -m "Release <version>"      # 8. create tag
git push origin <version>                        # 8. push tag
```
