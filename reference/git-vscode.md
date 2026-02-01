# Git in VS Code

Using Git through VS Code's Source Control panel — no command line required.

> **First time?** VS Code will prompt you to sign in to GitHub. Follow the prompts once and your credentials are saved.

---

## Cloning a Repository

When you accept a GitHub Classroom assignment, you get a repo URL. Here's how to clone it:

1. Copy the repo URL from GitHub (green **Code** button → HTTPS)
2. In VS Code: **View > Command Palette** (or `Cmd+Shift+P` / `Ctrl+Shift+P`)
3. Type `Git: Clone` and select it
4. Paste the URL and press Enter
5. Choose a folder to save it in
6. Click **Open** when prompted

Your repo is now open in VS Code.

---

## The Source Control Panel

Click the **Source Control icon** in the left sidebar (or press `Ctrl+Shift+G` / `Cmd+Shift+G`).

You'll see:
- **Changes** — Files you've modified
- **Staged Changes** — Files ready to commit
- **Message box** — Where you type your commit message

---

## Basic Workflow

### 1. Make changes to your code

Edit files normally. Changed files appear under **Changes** in the Source Control panel.

### 2. Stage your changes

- Click the **+** next to a file to stage it
- Or click the **+** next to **Changes** to stage all files

Staged files move to **Staged Changes**.

### 3. Commit

1. Type a message in the message box (e.g., "Add temperature converter")
2. Click the **checkmark** (✓) or press `Cmd+Enter` / `Ctrl+Enter`

Your changes are now saved locally.

### 4. Push to GitHub

Click the **...** menu in Source Control and select **Push**

Or use the **Sync** button (circular arrows) which does pull + push.

---

## Common Situations

### "I need to pull updates"

Click **...** → **Pull**

Or use the **Sync** button.

### "I see a number on the Source Control icon"

That's how many files have changed. Open the panel to see them.

### "I committed but forgot to push"

No problem — click **...** → **Push** (or Sync).

### "VS Code says there are merge conflicts"

This happens when you and someone else edited the same lines:
1. Open the conflicted file
2. VS Code highlights the conflicts
3. Choose **Accept Current**, **Accept Incoming**, or edit manually
4. Save the file
5. Stage and commit

### "I want to undo changes to a file"

Right-click the file in Source Control → **Discard Changes**

---

## Quick Reference

| Action | How |
|--------|-----|
| Open Source Control | Click sidebar icon or `Cmd/Ctrl+Shift+G` |
| Stage file | Click **+** next to file |
| Stage all | Click **+** next to Changes |
| Unstage file | Click **−** next to staged file |
| Commit | Type message, click ✓ |
| Push | **...** → Push |
| Pull | **...** → Pull |
| Sync (pull + push) | Click circular arrows |
| Discard changes | Right-click file → Discard Changes |
| View diff | Click a changed file |

---

## Tips

- **Commit often** — Small, frequent commits are easier to understand and undo
- **Write clear messages** — "Fix temperature calculation" beats "updates"
- **Pull before you start working** — Avoids merge conflicts
- **Check the status** — Glance at Source Control before closing VS Code
