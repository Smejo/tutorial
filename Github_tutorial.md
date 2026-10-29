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
