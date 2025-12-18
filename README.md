# Fast Memo – Project Documentation

## 1. Project Overview
- **Application name:** Fast Memo  
- **Purpose:** Lightweight note and memo manager with categories, search, and sorting.  
- **Problem solved:** Provides a quick way to create, view, edit, search, and organize memos with category filters and timestamps.  
- **Target users:** Students and professionals who need a simple, category-based note tool on Android.

## 2. Technology Stack
- **Language:** Java (Android)
- **Android SDK:** `compileSdk 36`, `targetSdk 36`, `minSdk 21`
- **Build tools:** Gradle (Kotlin DSL)
- **Libraries:**
  - AndroidX AppCompat, Material Components, Activity, ConstraintLayout, RecyclerView
  - Room (`room-runtime`, `room-compiler`) for local database
  - Lifecycle (`viewmodel`, `livedata`, `runtime`) for MVVM state
  - Security Crypto for encrypted shared preferences (PIN storage)
  - JUnit, AndroidX Test, Espresso for testing
- **Architecture pattern:** MVVM with Repository + Room

## 3. Project File Structure
```
app/
 ├─ src/main/java/com/example/notememo/
 │   ├─ SplashActivity.java          # Launcher splash screen
 │   ├─ MainActivity.java            # Home screen, list/search/filter/sort memos
 │   ├─ MemoEditorActivity.java      # Create/edit memo
 │   ├─ MemoDetailsActivity.java     # View memo details, delete/edit actions
 │   ├─ MemoAdapter.java             # RecyclerView adapter for memos
 │   ├─ MemoViewModel.java           # MVVM ViewModel, LiveData filters
 │   ├─ MemoRepository.java          # Data access layer, routes to DAO
 │   ├─ MemoDatabase.java            # Room database singleton
 │   ├─ MemoDao.java                 # Room DAO (queries and CRUD)
 │   ├─ Memo.java                    # Room entity/model
 │   └─ SecurityHelper.java          # PIN handling with encrypted prefs
 │
 ├─ res/
 │   ├─ layout/                      # XML UI layouts (main, list item, editor, details, splash, empty states)
 │   ├─ mipmap-*/                    # Launcher icons (adaptive + legacy)
 │   ├─ drawable/                    # App icon drawable wrappers, launcher assets
 │   ├─ values/                      # colors, strings, themes
 │   ├─ xml/                         # backup/data extraction rules
 │   └─ menu/                        # Toolbar and bottom navigation menus
 │
 ├─ AndroidManifest.xml              # App declaration, launcher, permissions, theme
 ├─ build.gradle.kts                 # App module Gradle config
 └─ proguard-rules.pro               # (unused minify off)
```

### Key folders and files
- **Activities**
  - `SplashActivity`: Shows branding for 2s then navigates to `MainActivity`.
  - `MainActivity`: Lists memos, handles search, category chips, sorting, empty states, and navigation to editor/details.
  - `MemoEditorActivity`: Creates or edits memos; supports category selection via dropdown (new) or chips (edit mode).
  - `MemoDetailsActivity`: Displays memo content, metadata, and supports edit/delete via toolbar.

- **Adapter**
  - `MemoAdapter`: Binds memo data to `RecyclerView` cards, formats timestamps, applies category colors.

- **Data layer**
  - `Memo`: Room entity with fields `uid`, `title`, `content`, `category`, `createdAt`, `updatedAt`.
  - `MemoDao`: Room queries for full list, category filters, search with sorting modes.
  - `MemoDatabase`: Singleton Room database with fallback-to-destructive migration.
  - `MemoRepository`: Exposes LiveData queries with sort/search/category routing; executes writes on background executor.

- **ViewModel**
  - `MemoViewModel`: Holds LiveData filters (search, category, sort), exposes memo list via MediatorLiveData, and CRUD passthroughs.

- **Utilities**
  - `SecurityHelper`: Manages PIN enable/verify using `EncryptedSharedPreferences` (with SHA-256 hashing fallback).

- **Resources**
  - Layouts: `activity_splash`, `activity_main`, `activity_memo_editor`, `activity_memo_editor_edit`, `activity_memo_details`, `item_memo`, `empty_search_state`.
  - Values: `colors.xml`, `strings.xml`, `themes.xml`.
  - Drawables: Adaptive icon layers (`app_icon_drawable`, `app_icon.png`), launcher backgrounds/foregrounds.
  - Menus: `main_menu` (sorting, pin), `toolbar_main`, `toolbar_details`, `bottom_navigation`.

## 4. Application Workflow
1. **Launch flow:**  
   - Launcher activity: `SplashActivity` (2-second delay) → `MainActivity`.
2. **MainActivity:**  
   - Shows search bar, category chips, memo list (`RecyclerView`), and empty states.  
   - FAB and “New Memo” buttons navigate to `MemoEditorActivity` for creation.  
   - Tapping a memo opens `MemoDetailsActivity`; long-press opens delete confirmation.
   - Toolbar menu: sorting (date asc/desc, category), PIN settings.
3. **MemoDetailsActivity:**  
   - Displays memo details; toolbar actions: edit (opens editor with memo ID) or delete (dialog).
4. **MemoEditorActivity:**  
   - New mode: basic fields + category dropdown.  
   - Edit mode: fields prefilled, chips to change category, shows last edited label.  
   - Save action updates or inserts via `MemoViewModel` → `Repository` → `Room`.
5. **Data flow:**  
   - UI events update `MemoViewModel` filters (search text, category chip, sort).  
   - `MemoViewModel` builds LiveData queries through `MemoRepository` → `MemoDao`.  
   - LiveData results update `RecyclerView` through `MemoAdapter`.  
   - CRUD writes go through Repository executor → DAO.

## 5. Core Logic Explanation
- **Search & filtering:** Text change on search bar calls `setSearchQuery`; category chips call `setSelectedCategory`; sorting menu calls `setSortMode`. `MemoViewModel` recomputes LiveData query, `MainActivity` shows list or empty search state.
- **Empty states:** `updateEmptyState` toggles between results, “no memos” placeholder, or “no matches” when searching.
- **List interaction:** Adapter binds memo title/content, category chip color, human-readable timestamp, and click/long-click listeners.
- **Editor logic:** Determines create vs edit from intent extra `memo_uid`; saves new memo or updates existing; updates timestamps via Repository.
- **Details logic:** Loads memo by ID, formats metadata and updated time, supports delete with confirmation dialog.
- **PIN handling:** `SecurityHelper` stores hashed PIN, with encrypted preferences when available; dialogs in `MainActivity` allow enable/disable/change.

## 6. Database & Data Management
- **Database:** Room (SQLite under the hood), database name `memo_database`.
- **Entity:** `Memo` with `uid (PK)`, `title`, `content`, `category`, `createdAt`, `updatedAt`.
- **DAO queries:**  
  - Get all memos (updated desc), sorted variants (created asc/desc, category).  
  - Filter by category with sort variants.  
  - Search by title/content with or without category, with sort variants.  
  - CRUD: insert (auto timestamps in Repository), update (updates `updatedAt`), delete.
- **Repository:** Chooses correct DAO query based on search text, category, sort mode; executes writes on background executor.

## 7. UI & UX Design
- **Layouts:**  
  - `activity_main`: toolbar, always-visible search bar, category chips, `RecyclerView`, empty states, FAB.  
  - `item_memo`: Card with title, preview, category chip, timestamp.  
  - `activity_memo_editor` / `_edit`: Input fields, category selection (dropdown or chips), save menu.  
  - `activity_memo_details`: Read-only view with metadata, category chip, edit/delete menu.  
  - `activity_splash`: Centered logo and app name.  
  - `empty_search_state`: Not-found messaging and clear-search button.
- **RecyclerView:** Used in `MainActivity` with `MemoAdapter`; DiffUtil for efficient updates.
- **Binding:** Uses `findViewById`; ViewBinding is enabled in Gradle but not used in code.

## 8. Android Manifest & Permissions
- **Launcher:** `SplashActivity` (MAIN + LAUNCHER) → `MainActivity`.  
- **Icons:** `@mipmap/ic_launcher`, `@mipmap/ic_launcher_round`.  
- **Theme:** `@style/Theme.NoteMemo`.  
- **Permissions:** None declared; app operates without runtime permissions.

## 9. Build & Execution Process
- **Gradle config:** Defined in `app/build.gradle.kts`; Java 11 compatibility; viewBinding enabled.  
- **Build tasks:** `assembleDebug` / `assembleRelease`; release minify disabled.  
- **APK output:** Standard Gradle outputs under `app/build/outputs/apk/`.

## 10. Error Handling & Debugging
- **Try-catch:** SecurityHelper falls back to normal SharedPreferences on encryption errors; hashing fallback returns raw PIN on exception (not secure but prevents crash).  
- **Dialogs for destructive actions:** Delete confirmations in main list (long-press) and details screen.  
- **Observers:** LiveData observers handle null/absent memo by finishing activity in `MemoDetailsActivity`.  
- **Logging:** No explicit logging present; rely on system logs for exceptions.

## 11. Conclusion
- **Summary:** Fast Memo is a category-driven memo app using MVVM, Room, and LiveData. It supports search, sorting, category filtering, creation/editing, and secure PIN gating.  
- **Strengths:** Clean MVVM separation, Room-powered offline storage, adaptive icons, splash experience, encrypted PIN storage, DiffUtil for list efficiency.  
- **Future improvements:** Add input validation and error messages, migrate to full ViewBinding/Compose, add tests, support attachments/media, improve localization and accessibility, and harden PIN hashing/error handling.

---
### Build & Run (quick)
```
./gradlew assembleDebug
```
Install the generated APK from `app/build/outputs/apk/debug/`.

