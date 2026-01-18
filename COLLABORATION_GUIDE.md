# Git Collaboration Guide for 5-Person Team

## Overview
This guide explains how 5 developers can work on the Fast Memo project simultaneously without conflicts using Git branching strategy.

---

## Step 1: Initial GitHub Setup

### Create GitHub Repository

1. Go to GitHub.com and create a new repository
2. Name it: `fast-memo` (or `noteMemo`)
3. **Do NOT initialize with README, .gitignore, or license** (we already have these)
4. Copy the repository URL (e.g., `https://github.com/username/fast-memo.git`)

### First Person (Team Lead) - Initial Push

```bash
# Navigate to project directory
cd c:\Users\Administrator\AndroidStudioProjects\noteMemo

# Initialize Git (if not already done)
git init

# Add all files
git add .

# Create initial commit
git commit -m "Initial commit: Fast Memo Android application"

# Add remote repository
git remote add origin https://github.com/username/fast-memo.git

# Push to main branch
git branch -M main
git push -u origin main
```

---

## Step 2: Divide Work Among 5 Team Members

### Work Division Strategy

#### **Person 1: Database & Data Layer**
**Branch**: `feature/database-layer`
**Responsibilities**:
- `Memo.java` (Entity)
- `MemoDatabase.java`
- `MemoDao.java`
- Database schema updates
- Testing database operations

**Files to Work On**:
- `app/src/main/java/com/example/notememo/Memo.java`
- `app/src/main/java/com/example/notememo/MemoDatabase.java`
- `app/src/main/java/com/example/notememo/MemoDao.java`

---

#### **Person 2: Repository & ViewModel**
**Branch**: `feature/repository-viewmodel`
**Responsibilities**:
- `MemoRepository.java`
- `MemoViewModel.java`
- Data flow logic
- Testing repository/ViewModel

**Files to Work On**:
- `app/src/main/java/com/example/notememo/MemoRepository.java`
- `app/src/main/java/com/example/notememo/MemoViewModel.java`

---

#### **Person 3: Main Activity & UI Components**
**Branch**: `feature/main-activity`
**Responsibilities**:
- `MainActivity.java`
- `MemoAdapter.java`
- `activity_main.xml`
- `item_memo.xml`
- Main screen UI/UX

**Files to Work On**:
- `app/src/main/java/com/example/notememo/MainActivity.java`
- `app/src/main/java/com/example/notememo/MemoAdapter.java`
- `app/src/main/res/layout/activity_main.xml`
- `app/src/main/res/layout/item_memo.xml`
- `app/src/main/res/layout/empty_search_state.xml`

---

#### **Person 4: Editor & Details Activities**
**Branch**: `feature/editor-details`
**Responsibilities**:
- `MemoEditorActivity.java`
- `MemoDetailsActivity.java`
- Editor and details layouts
- Navigation between screens

**Files to Work On**:
- `app/src/main/java/com/example/notememo/MemoEditorActivity.java`
- `app/src/main/java/com/example/notememo/MemoDetailsActivity.java`
- `app/src/main/res/layout/activity_memo_editor.xml`
- `app/src/main/res/layout/activity_memo_editor_edit.xml`
- `app/src/main/res/layout/activity_memo_details.xml`

---

#### **Person 5: Security & Launch Screen**
**Branch**: `feature/security-splash`
**Responsibilities**:
- `SplashActivity.java`
- `SecurityHelper.java`
- Splash screen layout
- PIN security implementation
- Testing security features

**Files to Work On**:
- `app/src/main/java/com/example/notememo/SplashActivity.java`
- `app/src/main/java/com/example/notememo/SecurityHelper.java`
- `app/src/main/res/layout/activity_splash.xml`

---

## Step 3: Git Workflow for Each Team Member

### Setup for Each Person (Run Once)

```bash
# Clone the repository (Person 2, 3, 4, 5 only - Person 1 already has it)
git clone https://github.com/username/fast-memo.git
cd fast-memo

# Create your feature branch
# Person 1: git checkout -b feature/database-layer
# Person 2: git checkout -b feature/repository-viewmodel
# Person 3: git checkout -b feature/main-activity
# Person 4: git checkout -b feature/editor-details
# Person 5: git checkout -b feature/security-splash

# Push your branch to GitHub
git push -u origin feature/your-branch-name
```

---

### Daily Workflow for Each Person

#### Morning: Start Working

```bash
# 1. Fetch latest changes from GitHub
git fetch origin

# 2. Switch to main branch and update it
git checkout main
git pull origin main

# 3. Switch back to your feature branch
git checkout feature/your-branch-name

# 4. Merge latest main into your branch (to stay updated)
git merge main
# If conflicts occur, resolve them (see conflict resolution below)

# 5. Now you can work on your files
```

#### During Work: Make Changes

```bash
# Make changes to your assigned files
# Test your changes locally

# Stage your changes
git add app/src/main/java/com/example/notememo/YourFile.java

# Commit with descriptive message
git commit -m "feat: [Your feature] - description of changes"

# Example:
# Person 1: git commit -m "feat: database - add category filtering to MemoDao"
# Person 3: git commit -m "feat: main-activity - implement search functionality"
```

#### Before Pushing: Pull Latest Changes

```bash
# Always pull latest main before pushing
git checkout main
git pull origin main
git checkout feature/your-branch-name
git merge main

# Then push your branch
git push origin feature/your-branch-name
```

---

## Step 4: Merging Branches (Safe Approach)

### Option A: Sequential Merge (Recommended for First Time)

Merge branches one at a time to avoid conflicts:

```bash
# Step 1: Merge Person 1's branch (Database Layer) - Base layer, no dependencies
git checkout main
git pull origin main
git merge feature/database-layer
git push origin main

# Step 2: Merge Person 2's branch (Repository/ViewModel) - Depends on Database
git checkout main
git pull origin main
git merge feature/repository-viewmodel
git push origin main

# Step 3: Merge Person 5's branch (Security/Splash) - Independent
git checkout main
git pull origin main
git merge feature/security-splash
git push origin main

# Step 4: Merge Person 3's branch (Main Activity) - Depends on Repository/ViewModel
git checkout main
git pull origin main
git merge feature/main-activity
git push origin main

# Step 5: Merge Person 4's branch (Editor/Details) - Depends on Main Activity
git checkout main
git pull origin main
git merge feature/editor-details
git push origin main
```

### Option B: Parallel Development with Regular Sync

All team members merge their branches frequently:

```bash
# Each person should do this daily:
git checkout main
git pull origin main
git checkout feature/your-branch-name
git merge main  # Merge main into your branch to stay updated
git push origin feature/your-branch-name
```

---

## Step 5: Handling Merge Conflicts

### When Conflicts Occur

1. **Identify Conflicting Files**:
```bash
git status
# Shows files with conflicts marked as "both modified"
```

2. **Open Conflicting Files**:
```bash
# Git marks conflicts like this:
<<<<<<< HEAD
// Code from main branch (or your branch)
=======
// Code from branch being merged
>>>>>>> feature/other-branch
```

3. **Resolve Conflicts**:
   - Keep both changes if compatible
   - Keep only one version if duplicate
   - Combine changes if needed
   - Remove conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`)

4. **Example Conflict Resolution**:

```java
// BEFORE (with conflict):
<<<<<<< HEAD
    public void searchMemos(String query) {
        return memoDao.searchMemos(query);
    }
=======
    public LiveData<List<Memo>> searchMemos(String query) {
        return memoDao.searchMemos(query);
    }
>>>>>>> feature/repository-viewmodel

// AFTER (resolved - Person 2's version is correct):
    public LiveData<List<Memo>> searchMemos(String query) {
        return memoDao.searchMemos(query);
    }
```

5. **Complete the Merge**:
```bash
# After resolving all conflicts:
git add .
git commit -m "merge: resolve conflicts with feature/other-branch"
git push origin feature/your-branch-name
```

---

## Step 6: Pull Requests (Recommended for Team Work)

### Why Use Pull Requests?

- Code review before merging
- Discussion about changes
- Automatic testing (if configured)
- Better history tracking

### Create Pull Request

1. **Each person pushes their branch**:
```bash
git push origin feature/your-branch-name
```

2. **Go to GitHub**:
   - Click "Pull Requests" tab
   - Click "New Pull Request"
   - Select: `main` ← `feature/your-branch-name`
   - Add title: `feat: [Feature Name] - Description`
   - Add description of changes
   - Request review from team members
   - Click "Create Pull Request"

3. **Review Process**:
   - Team members review code
   - Discuss changes in comments
   - Request changes if needed

4. **Merge Pull Request**:
   - Click "Merge Pull Request"
   - Select "Squash and merge" or "Create a merge commit"
   - Confirm merge

---

## Step 7: Conflict Prevention Strategies

### 1. Work on Different Files
- Each person works on different files (as divided above)
- This minimizes conflicts

### 2. Communicate Changes
- Use team chat/Slack/Discord to communicate
- Announce: "I'm working on MainActivity.java now"
- Others avoid that file while you're working

### 3. Small, Frequent Commits
```bash
# Good: Small commits
git commit -m "feat: add search input field"
git commit -m "feat: implement search TextWatcher"

# Bad: One huge commit with all changes
git commit -m "feat: complete MainActivity implementation"
```

### 4. Regular Pulls from Main
```bash
# Do this multiple times per day:
git checkout main
git pull origin main
git checkout feature/your-branch-name
git merge main
```

### 5. Coordinate Shared Files
If multiple people need to edit same file:
- Discuss approach first
- Person 1 makes changes → commits → pushes
- Person 2 pulls latest → makes their changes → commits → pushes

---

## Step 8: Testing Before Merge

### Each Person Should Test:

```bash
# 1. Build the project
./gradlew clean build

# 2. Run on emulator/device
# Test your specific features

# 3. Test integration with other parts (if possible)
```

### Merge Test:

```bash
# After merging to main, test entire app:
git checkout main
git pull origin main

# Build and test complete app
./gradlew clean build
# Run full app test
```

---

## Step 9: Emergency Fixes (Hotfixes)

### If Bug Found in Main Branch:

```bash
# Create hotfix branch from main
git checkout main
git pull origin main
git checkout -b hotfix/bug-description

# Fix the bug
# Commit fix
git commit -m "fix: description of bug fix"

# Push and create PR to merge into main immediately
git push origin hotfix/bug-description
```

---

## Step 10: Final Merge Checklist

Before final merge, verify:

- [ ] All branches are up to date with main
- [ ] All conflicts resolved
- [ ] Code compiles without errors
- [ ] All features tested individually
- [ ] Integration tested (app runs end-to-end)
- [ ] No merge conflicts remaining
- [ ] All team members' work is included

---

## Quick Reference Commands

### For Each Team Member

```bash
# Start day
git checkout main
git pull origin main
git checkout feature/your-branch-name
git merge main

# During work
git add .
git commit -m "feat: your change description"
git push origin feature/your-branch-name

# End of day
git checkout main
git pull origin main
git checkout feature/your-branch-name
git merge main
git push origin feature/your-branch-name
```

### For Team Lead (Merging to Main)

```bash
# Merge feature branch
git checkout main
git pull origin main
git merge feature/team-member-branch
git push origin main

# Notify team to update their branches
```

---

## Branch Naming Convention

Use this naming pattern:
- `feature/your-feature-name` - New features
- `bugfix/bug-description` - Bug fixes
- `hotfix/critical-fix` - Urgent fixes
- `refactor/component-name` - Code refactoring

Examples:
- `feature/database-layer`
- `feature/main-activity-search`
- `bugfix/category-filter-error`
- `hotfix/pin-security-fix`

---

## Common Issues & Solutions

### Issue 1: "Your branch is behind 'origin/main'"
**Solution**:
```bash
git checkout main
git pull origin main
git checkout feature/your-branch-name
git merge main
```

### Issue 2: "Merge conflict in build.gradle.kts"
**Solution**: Usually happens when dependencies change
- Compare both versions
- Keep all dependencies (combine them)
- Keep version numbers from latest change

### Issue 3: "Cannot push - branch is protected"
**Solution**: 
- Create Pull Request instead
- Or ask team lead to merge your branch

### Issue 4: "Someone else pushed while I was working"
**Solution**:
```bash
git pull origin feature/your-branch-name
# Resolve conflicts if any
git push origin feature/your-branch-name
```

---

## Recommended Workflow Timeline

### Week 1: Setup & Division
- Day 1: Setup GitHub repo, create branches
- Day 2-3: Each person works on their files
- Day 4: First merge (Person 1: Database layer)
- Day 5: Second merge (Person 2: Repository/ViewModel)

### Week 2: Development & Integration
- Day 1: Merge Person 5 (Security/Splash)
- Day 2: Merge Person 3 (Main Activity)
- Day 3: Merge Person 4 (Editor/Details)
- Day 4: Integration testing
- Day 5: Bug fixes and final testing

---

## Team Communication Template

### When Starting Work:
```
"I'm starting work on [feature/component]. 
Will be editing [list of files]. 
Estimated completion: [time]"
```

### Before Pushing:
```
"Pushing changes to feature/[branch-name]. 
Changed [list of files]. 
Ready for review/test."
```

### When Conflicts Occur:
```
"Merge conflict in [filename]. 
Need help resolving. 
Conflicts are: [description]"
```

---

## Summary

1. **Each person works on separate branch**: `feature/your-assignment`
2. **Regular sync with main**: Pull main → merge into your branch → push
3. **Work on different files**: Minimizes conflicts
4. **Small commits**: Easier to track and merge
5. **Test before merge**: Ensure code compiles and works
6. **Use Pull Requests**: Better code review and history

**Key Principle**: Stay updated with main branch regularly to avoid large conflicts!

---

**Questions?** Contact team lead or refer to Git documentation.
