# 🐙 Git & GitHub Master Guide

> **Topics Covered:** What is Git vs GitHub?, Commit, Branch, Merge vs Rebase, Pull Requests & Code Review, Resolving Merge Conflicts, `git fetch` vs `git pull`, `git reset` vs `git revert`, `git stash`, `git cherry-pick`, `.gitignore`, HEAD & Detached HEAD, `git reflog`, Undoing Commits, Git Squash, Fork vs Clone.

---

### Q1: Git vs GitHub & Merge vs Rebase ⭐⭐
**Question:** What is Git vs GitHub? What is the difference between `git merge` and `git rebase`?

**Answer:**
- **Git**: Local Distributed Version Control System (VCS) tool running on your terminal.
- **GitHub**: Cloud-based hosting platform for Git repositories providing collaboration, PRs, and CI/CD (GitHub Actions).
- **`git merge` vs `git rebase`:**
  - **`git merge`**: Creates a new **Merge Commit** combining two branch histories. Preserves complete, non-destructive chronological branch history.
  - **`git rebase`**: Moves the entire feature branch to begin on the tip of the target branch, rewriting commit history to create a **clean, linear commit timeline**.
  - *Golden Rule:* Never rebase public shared branches!

```bash
# Merge:
git checkout main
git merge feature-branch

# Rebase:
git checkout feature-branch
git rebase main
```

---

### Q2: `git fetch` vs `git pull` & `git reset` vs `git revert`
**Question:** Compare `git fetch` vs `git pull` and `git reset` vs `git revert`.

**Answer:**
- **`git fetch` vs `git pull`**:
  - `git fetch`: Downloads all new commits, branches, and tags from remote repository to your local repo, but **does not modify your working directory**.
  - `git pull`: Runs `git fetch` followed immediately by `git merge` into your current working branch.
- **`git reset` vs `git revert`**:
  - **`git reset <commit>`**: Moves the HEAD pointer backward, rewriting history (Destructive). `--soft` (keeps changes staged), `--hard` (discards all changes).
  - **`git revert <commit>`**: Creates a **brand new commit** that introduces the exact inverse diff of the target commit. Safe for public shared branches.

---

### Q3: How Do You Undo the Last Commit or a Pushed Commit?
**Question:** What commands do you run to undo a local commit vs an already pushed commit?

**Answer:**
```bash
# 1. Undo local commit but keep all modified code unstaged in files:
git reset HEAD~1

# 2. Undo local commit and discard all changes permanently:
git reset --hard HEAD~1

# 3. Undo an already pushed remote commit safely:
git revert <commit-hash>
git push origin main
```

---

### Q4: What is `git reflog` and How Does It Save Lost Work?
**Question:** What is `git reflog`? How can you recover commits accidentally deleted by `git reset --hard`?

**Answer:**
- **`git reflog` (Reference Log)**: Records every single movement of the `HEAD` pointer locally in your repository (including resets, checkouts, and deleted branches).
- **Recovery Steps:**
  1. Run `git reflog` to find the SHA hash of the lost commit.
  2. Run `git checkout <sha>` or `git branch recovery-branch <sha>`.
