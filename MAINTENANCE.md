# Portfolio Maintenance Guide

Use this quick checklist whenever you refresh the portfolio locally and want those updates to appear on GitHub.

## 1. Sync the Latest Changes
1. Open a terminal in the repository folder.
2. Confirm you are on the branch that mirrors GitHub (usually `main`):
   ```bash
   git status -sb
   ```
   If you see `## main`, you are good to go. Otherwise, switch branches:
   ```bash
   git switch main
   ```
3. Pull down any remote updates so your local copy matches GitHub:
   ```bash
   git pull origin main
   ```

## 2. Stage and Commit Your Work
1. Review the files you modified:
   ```bash
   git status -sb
   ```
2. Stage the ones you want to publish:
   ```bash
   git add <file-or-folder>
   ```
   Use `git add .` if you are confident that every change should go live.
3. Create a descriptive commit message so the history stays clear:
   ```bash
   git commit -m "Describe what changed"
   ```

## 3. Push to GitHub
Send the committed updates to the remote repository:
```bash
git push origin main
```
GitHub will update within a few seconds. Refresh the repo page and confirm that the latest commit appears at the top.

## 4. Troubleshooting Tips
- **Nothing changes after pushing?** Make sure you are pushing to the correct repository/branch. Run `git remote -v` to double-check the URL.
- **Conflicts when pulling?** Resolve the conflicting files locally, then repeat the add/commit/push steps.
- **Need to undo a commit?** Use `git log --oneline` to find the commit hash, then run `git revert <hash>` to create a new commit that undoes it.

Keep this guide handy so future updates reach your GitHub portfolio smoothly.
