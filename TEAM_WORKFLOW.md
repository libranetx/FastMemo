# Quick Start: 5-Person Team Git Workflow

## 🎯 Work Assignment Summary

| Person | Branch Name | Main Files | Dependencies |
|--------|-------------|------------|--------------|
| **Person 1** | `feature/database-layer` | Memo.java, MemoDatabase.java, MemoDao.java | None (base layer) |
| **Person 2** | `feature/repository-viewmodel` | MemoRepository.java, MemoViewModel.java | Depends on Person 1 |
| **Person 3** | `feature/main-activity` | MainActivity.java, MemoAdapter.java, layouts | Depends on Person 2 |
| **Person 4** | `feature/editor-details` | MemoEditorActivity.java, MemoDetailsActivity.java | Depends on Person 3 |
| **Person 5** | `feature/security-splash` | SplashActivity.java, SecurityHelper.java | Independent |

---

## 📊 Visual Workflow

```
                    main branch
                        |
        ┌───────────────┼───────────────┐
        |               |               |
    Person 1       Person 5       Person 2
   (Database)   (Security)   (Repository)
        |               |               |
        └───────────────┼───────────────┘
                        |
                   main (after merge)
                        |
        ┌───────────────┼───────────────┐
        |                               |
    Person 3                       Person 4
(Main Activity)               (Editor/Details)
        |                               |
        └───────────────┼───────────────┘
                        |
                   main (final)
```

---

## 🚀 One-Time Setup (Each Person)

### Step 1: Clone Repository (Persons 2-5 only)
```bash
git clone https://github.com/username/fast-memo.git
cd fast-memo
```

### Step 2: Create Your Branch

```bash
# Person 1 (already has repo):
git checkout -b feature/database-layer
git push -u origin feature/database-layer

# Person 2:
git checkout -b feature/repository-viewmodel
git push -u origin feature/repository-viewmodel

# Person 3:
git checkout -b feature/main-activity
git push -u origin feature/main-activity

# Person 4:
git checkout -b feature/editor-details
git push -u origin feature/editor-details

# Person 5:
git checkout -b feature/security-splash
git push -u origin feature/security-splash
```

---

## 💻 Daily Work Commands (Copy & Paste)

### Morning Routine
```bash
# 1. Get latest from main
git checkout main
git pull origin main

# 2. Update your branch with main
git checkout feature/YOUR-BRANCH-NAME
git merge main

# 3. Start working
```

### During Work
```bash
# Make changes to files...

# Save your work
git add app/src/main/java/com/example/notememo/YourFile.java
git commit -m "feat: your feature - what you changed"
git push origin feature/YOUR-BRANCH-NAME
```

### End of Day
```bash
# Final sync
git checkout main
git pull origin main
git checkout feature/YOUR-BRANCH-NAME
git merge main
git push origin feature/YOUR-BRANCH-NAME
```

---

## 🔄 Merge Order (Important!)

Merge in this exact order to avoid conflicts:

1. ✅ **Person 1** → `feature/database-layer` (Base layer)
2. ✅ **Person 2** → `feature/repository-viewmodel` (Needs database)
3. ✅ **Person 5** → `feature/security-splash` (Independent)
4. ✅ **Person 3** → `feature/main-activity` (Needs repository)
5. ✅ **Person 4** → `feature/editor-details` (Needs main activity)

---

## 📝 Merge to Main (Team Lead or Person 1)

```bash
# For each merge:
git checkout main
git pull origin main
git merge feature/BRANCH-NAME
git push origin main

# After pushing main, notify team:
# "Main updated! Please sync your branches: git checkout main && git pull && git checkout YOUR-BRANCH && git merge main"
```

---

## ⚠️ Conflict Resolution Quick Guide

If you see conflicts:

1. **Open the conflicted file**
2. **Look for markers**:
   ```
   <<<<<<< HEAD
   (code from main)
   =======
   (code from your branch)
   >>>>>>> feature/your-branch
   ```
3. **Keep the correct code** (or combine both)
4. **Remove the markers** (`<<<<<<<`, `=======`, `>>>>>>>`)
5. **Save and commit**:
   ```bash
   git add .
   git commit -m "merge: resolved conflicts"
   git push origin feature/YOUR-BRANCH-NAME
   ```

---

## 📋 File Edit Checklist

Before editing a file, check if someone else is working on it:

✅ **Safe to edit** if:
- It's in your assigned files list
- No one announced they're working on it
- You checked team chat

❌ **Don't edit** if:
- Someone is currently working on it
- It's outside your assignment
- It's not in your branch's responsibility

---

## 🆘 Emergency Commands

### I messed up my branch!
```bash
# Reset to last good commit (CAREFUL - loses uncommitted changes)
git reset --hard origin/feature/YOUR-BRANCH-NAME

# Or reset to main
git checkout main
git branch -D feature/YOUR-BRANCH-NAME
git checkout -b feature/YOUR-BRANCH-NAME
```

### I need to undo my last commit
```bash
# Undo commit but keep changes
git reset --soft HEAD~1

# Undo commit and changes (CAREFUL)
git reset --hard HEAD~1
```

### My branch is completely broken
```bash
# Start fresh from main
git checkout main
git pull origin main
git branch -D feature/YOUR-BRANCH-NAME
git checkout -b feature/YOUR-BRANCH-NAME
# Start working again
```

---

## ✅ Pre-Merge Checklist

Before merging your branch to main:

- [ ] Code compiles: `./gradlew clean build`
- [ ] App runs on emulator/device
- [ ] Your features work correctly
- [ ] No merge conflicts with main
- [ ] All team members' branches are synced
- [ ] All tests pass (if any)

---

## 📞 Communication Template

### Starting work:
```
👋 Starting work on [component]
📝 Editing: [file names]
⏰ ETA: [time]
```

### Pushing changes:
```
✅ Pushed changes to feature/[branch]
📦 Files changed: [list]
🔍 Ready for review
```

### Need help:
```
❓ Need help with [issue]
📁 File: [filename]
💭 Problem: [description]
```

---

## 🎓 Key Rules

1. **Always pull main before starting work**
2. **Commit frequently** (small commits are better)
3. **Push regularly** (at least once per day)
4. **Communicate changes** (let team know what you're editing)
5. **Test before merge** (ensure code works)
6. **Resolve conflicts immediately** (don't let them pile up)

---

## 📚 Quick Reference

| Command | What It Does |
|---------|--------------|
| `git status` | See what files changed |
| `git log` | See commit history |
| `git branch` | List all branches |
| `git checkout BRANCH` | Switch to branch |
| `git pull` | Get latest from GitHub |
| `git push` | Send your changes to GitHub |
| `git merge BRANCH` | Combine branches |
| `git add .` | Stage all changes |
| `git commit -m "message"` | Save changes |

---

**Remember**: Stay synced with main, commit often, communicate with team! 🚀
