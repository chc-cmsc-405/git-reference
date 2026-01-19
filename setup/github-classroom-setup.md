# GitHub Classroom Setup

How to set up GitHub and work with assignments using GitHub Classroom.

---

# Required Setup

Complete this step before the first assignment.

## GitHub Account

**Already have a GitHub account?** You're all set — skip to Assignment Workflow below.

**Need to create one?**

1. Go to: https://github.com/signup
2. Use any email address (personal or school — either is fine)
3. Choose a professional username (employers may see this)
4. Verify your email address

---

# Assignment Workflow

## Accept an Assignment

1. Click the assignment link provided in Canvas
2. Accept the assignment (this creates your personal repository)

## Clone Your Repository

In VS Code:
1. Open Command Palette (`Ctrl+Shift+P` / `Cmd+Shift+P`)
2. Type "Git: Clone" and press Enter
3. Select "Clone from GitHub"
4. If prompted, sign in to GitHub in your browser (first time only)
5. Find and select your assignment repository
6. Choose a local folder to save the project

## Make and Save Changes

1. Edit files in VS Code as you work
2. Click the **Source Control** icon in the left sidebar (branch icon)
3. Review your changes
4. Click `+` next to files to stage them (or `+` next to "Changes" for all)
5. Type a commit message describing your changes
6. Click the checkmark to commit
7. Click "Sync Changes" to push to GitHub

Your submission is timestamped when you push. You can push multiple times before the deadline.

---

## Submission Checklist

Before the deadline:

- [ ] All files saved
- [ ] Changes staged (click `+`)
- [ ] Changes committed (checkmark)
- [ ] Changes pushed ("Sync Changes")
- [ ] Verify on GitHub.com that your latest code is there

---

## Viewing Autograding Results

Most assignments include automated tests that run when you push your code. To see your results:

1. Go to your repository on GitHub.com
2. Click the **Actions** tab
3. Look for the most recent workflow run:
   - ✅ Green checkmark = all tests passed
   - ❌ Red X = one or more tests failed
4. Click on the workflow run to see details
5. Click on "Autograding" to see your score breakdown

**If tests fail:**
- Click into the failed job to see the error message
- Fix the issue in VS Code
- Commit and push again — tests run automatically on each push
- You can push as many times as needed before the deadline

---

## VS Code Git Integration

| Action | How |
|--------|-----|
| Open Source Control | Click branch icon in left sidebar (or `Ctrl+Shift+G`) |
| Stage file | Click `+` next to file |
| Stage all | Click `+` next to "Changes" header |
| Commit | Type message, click checkmark (or `Ctrl+Enter`) |
| Push | Click "Sync Changes" or `...` menu → Push |
| Pull | Click "Sync Changes" or `...` menu → Pull |

---

# Optional

## Configure Git Identity

By default, commits show your computer's username. To display your actual name:

1. Open a terminal in VS Code (`Ctrl+`` ` or `Cmd+`` `)
2. Run:
   ```bash
   git config --global user.name "Your Name"
   git config --global user.email "your.email@example.com"
   ```

This is cosmetic — it only affects how your name appears in commit history. It doesn't affect grading or submissions.

---

## Command Line Users

Prefer working in the terminal? See [Git Reference](git-reference.md) for command-line workflow.
