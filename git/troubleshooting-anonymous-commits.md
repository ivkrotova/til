# How to Fix Anonymous GitHub Commits

If the commits you made are showing up as anonymous or not linked to your GitHub account, this is how to fix it.

## 1. Verify Your GitHub Email

1. Go to GitHub Settings → Emails (https://github.com/settings/emails)
2. Note your primary email address
3. Make sure it's verified (if not, verify it first)

## 2. Check Your Local Git Configuration

```bash
git config --list

git config user.email
git config user.name
```

## 3. Set Correct Configuration

```bash
# Set the name and email for the current repository
git config user.name "Your-GitHub-Username"
git config user.email "your-verified-github-email@example.com"

# Or set globally for all repositories
git config --global user.name "Your-GitHub-Username"
git config --global user.email "your-verified-github-email@example.com"
```

## 4. Fix Existing Commits

### Fix Last Commit Only
```bash
# Amend the last commit with correct author info
git commit --amend --reset-author --no-edit
git push -f origin main
```

### Fix Multiple Recent Commits
```bash
# Replace N with the number of commits to fix
git rebase -i HEAD~N
```
Then change `pick` to `edit` for each commit you want to modify, and for each commit:
```bash
git commit --amend --reset-author --no-edit
git rebase --continue
```

### Fix All Commits in Repository
```bash
git filter-branch -f --env-filter '
    GIT_AUTHOR_NAME="Your-GitHub-Username"
    GIT_AUTHOR_EMAIL="your-verified-github-email@example.com"
    GIT_COMMITTER_NAME="Your-GitHub-Username"
    GIT_COMMITTER_EMAIL="your-verified-github-email@example.com"
' HEAD

# Force push the changes
git push -f origin main
```

## Important Notes

Using `git push -f` rewrites history - use with caution on shared repositories