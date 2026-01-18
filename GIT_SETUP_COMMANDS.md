# Quick Git Setup Commands for 5-Person Team

## 🎯 For Person 1 (Team Lead / Has Existing Code)

```bash
# Navigate to project
cd c:\Users\Administrator\AndroidStudioProjects\noteMemo

# Initialize Git (if not done)
git init

# Add all files
git add .

# First commit
git commit -m "Initial commit: Fast Memo Android application"

# Add GitHub remote (replace with your actual URL)
git remote add origin https://github.com/YOUR-USERNAME/fast-memo.git

# Create main branch and push
git branch -M main
git push -u origin main

# Create your feature branch
git checkout -b feature/database-layer
git push -u origin feature/database-layer
```

---

## 🎯 For Person 2 (Repository/ViewModel)

```bash
# Clone repository
git clone https://github.com/YOUR-USERNAME/fast-memo.git
cd fast-memo

# Create your feature branch
git checkout -b feature/repository-viewmodel
git push -u origin feature/repository-viewmodel

# Start working on:
# - MemoRepository.java
# - MemoViewModel.java
```

---

## 🎯 For Person 3 (Main Activity)

```bash
# Clone repository
git clone https://github.com/YOUR-USERNAME/fast-memo.git
cd fast-memo

# Create your feature branch
git checkout -b feature/main-activity
git push -u origin feature/main-activity

# Start working on:
# - MainActivity.java
# - MemoAdapter.java
# - activity_main.xml
# - item_memo.xml
```

---

## 🎯 For Person 4 (Editor/Details)

```bash
# Clone repository
git clone https://github.com/YOUR-USERNAME/fast-memo.git
cd fast-memo

# Create your feature branch
git checkout -b feature/editor-details
git push -u origin feature/editor-details

# Start working on:
# - MemoEditorActivity.java
# - MemoDetailsActivity.java
# - activity_memo_editor.xml
# - activity_memo_details.xml
```

---

## 🎯 For Person 5 (Security/Splash)

```bash
# Clone repository
git clone https://github.com/YOUR-USERNAME/fast-memo.git
cd fast-memo

# Create your feature branch
git checkout -b feature/security-splash
git push -u origin feature/security-splash

# Start working on:
# - SplashActivity.java
# - SecurityHelper.java
# - activity_splash.xml
```

---

## 📋 Daily Work Commands (All Team Members)

### Morning Setup (Run Every Day)
```bash
# Get latest main branch
git checkout main
git pull origin main

# Update your branch with main
git checkout feature/YOUR-BRANCH-NAME
git merge main

# If conflicts occur, resolve them:
# - Open conflicted files
# - Resolve conflicts manually
# - Then: git add . && git commit -m "merge: resolved conflicts"
```

### During Work (Commit Frequently)
```bash
# After making changes:
git add app/src/main/java/com/example/notememo/YourFile.java
git commit -m "feat: description of your changes"
git push origin feature/YOUR-BRANCH-NAME
```

### Before Pushing (Stay Updated)
```bash
# Always sync with main before pushing
git checkout main
git pull origin main
git checkout feature/YOUR-BRANCH-NAME
git merge main
git push origin feature/YOUR-BRANCH-NAME
```

---

## 🔄 Merge to Main (Team Lead Only)

Merge branches in this order:

```bash
# 1. Merge Person 1 (Database Layer)
git checkout main
git pull origin main
git merge feature/database-layer
git push origin main

# 2. Merge Person 2 (Repository/ViewModel)
git checkout main
git pull origin main
git merge feature/repository-viewmodel
git push origin main

# 3. Merge Person 5 (Security/Splash)
git checkout main
git pull origin main
git merge feature/security-splash
git push origin main

# 4. Merge Person 3 (Main Activity)
git checkout main
git pull origin main
git merge feature/main-activity
git push origin main

# 5. Merge Person 4 (Editor/Details)
git checkout main
git pull origin main
git merge feature/editor-details
git push origin main
```

**After each merge, notify team:**
```
"✅ Main updated! Please sync: 
git checkout main && git pull && 
git checkout feature/YOUR-BRANCH && 
git merge main"
```

---

## ⚠️ Conflict Resolution

If you get conflicts when merging:

```bash
# 1. See which files have conflicts
git status

# 2. Open conflicted files and look for:
<<<<<<< HEAD
(code from main)
=======
(code from your branch)
>>>>>>> feature/your-branch

# 3. Edit files - keep correct code, remove markers

# 4. After resolving all conflicts:
git add .
git commit -m "merge: resolved conflicts"
git push origin feature/YOUR-BRANCH-NAME
```

---

## 🔍 Useful Commands

```bash
# See current branch
git branch

# See what files changed
git status

# See commit history
git log --oneline

# Discard uncommitted changes (CAREFUL!)
git checkout -- filename.java

# See difference from main
git diff main..feature/YOUR-BRANCH-NAME
```

---

## ✅ Pre-Push Checklist

Before pushing your branch:

- [ ] Code compiles: `./gradlew clean build` (or `gradlew.bat clean build` on Windows)
- [ ] Your changes work (test on emulator/device)
- [ ] Merged latest main into your branch
- [ ] Committed all your changes
- [ ] Written clear commit messages

---

## 📞 Need Help?

- **Merge conflicts?** → Check COLLABORATION_GUIDE.md Section 5
- **Lost changes?** → Check TEAM_WORKFLOW.md Emergency Commands
- **Can't push?** → Make sure you committed changes first: `git commit -m "message"`
- **Branch deleted?** → Recreate: `git checkout -b feature/YOUR-BRANCH-NAME`

---

**Remember**: 
- ✅ Pull main regularly
- ✅ Commit small, frequent changes
- ✅ Communicate with team
- ✅ Test before merge
