# Git Command Reference

Command-line Git reference for students who prefer working in the terminal.

> **First time pushing?** Git will open a browser window to authenticate with GitHub. Log in once and your credentials are saved for future use.

---

## Basic Workflow

```bash
git status              # See what's changed
git add .               # Stage all changes
git commit -m "message" # Save changes locally
git push                # Upload to GitHub
git pull                # Download from GitHub
```

---

## Checking Status

**See changed and staged files:**
```bash
git status
```

**See commit history:**
```bash
git log --oneline
```

**See what you changed (unstaged):**
```bash
git diff
```

**See what you're about to commit (staged):**
```bash
git diff --staged
```

---

## Common Situations

### "I made changes but forgot to commit"

```bash
git add .
git commit -m "Your message"
git push
```

### "I need to pull instructor updates"

```bash
git pull
```

### "Git says I have uncommitted changes and won't let me pull"

Commit your changes first, then pull:
```bash
git add .
git commit -m "Save my work"
git pull
```

### "I accidentally edited the wrong file"

Discard changes to a specific file:
```bash
git checkout -- filename.cpp
```

### "I want to undo my last commit (before pushing)"

```bash
git reset --soft HEAD~1
```
Your changes stay staged; you can edit and recommit.

### "I need to see what changed in a specific commit"

```bash
git show <commit-hash>
```

---

## Command Reference

| Command | What it does |
|---------|--------------|
| `git clone <url>` | Download a repo to your computer |
| `git status` | Show changed/staged files |
| `git add <file>` | Stage a specific file |
| `git add .` | Stage all changed files |
| `git commit -m "msg"` | Save staged changes with message |
| `git push` | Upload commits to GitHub |
| `git pull` | Download updates from GitHub |
| `git log --oneline` | Show commit history (compact) |
| `git log` | Show commit history (detailed) |
| `git diff` | Show unstaged changes |
| `git diff --staged` | Show staged changes |
| `git show <hash>` | Show a specific commit |
| `git checkout -- <file>` | Discard changes to a file |
| `git reset --soft HEAD~1` | Undo last commit, keep changes staged |
| `git branch` | List branches |
| `git remote -v` | Show remote repository URL |

---

## Configuration

**Set your identity (run once per computer):**
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

**Check your current config:**
```bash
git config --list
```
