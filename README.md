# Fast Memo - Complete Project Documentation

## Table of Contents
1. [Project Overview](#1-project-overview)
2. [Technology Stack](#2-technology-stack)
3. [Project File Structure](#3-project-file-structure)
4. [Application Workflow](#4-application-workflow)
5. [Core Logic Explanation](#5-core-logic-explanation)
6. [Database & Data Management](#6-database--data-management)
7. [UI & UX Design](#7-ui--ux-design)
8. [Android Manifest & Permissions](#8-android-manifest--permissions)
9. [Build & Execution Process](#9-build--execution-process)
10. [Error Handling & Debugging](#10-error-handling--debugging)
11. [Conclusion](#11-conclusion)

---

## 1. Project Overview

### Application Name
**Fast Memo** (NoteMemo)

### Purpose of the App
Fast Memo is a modern Android note-taking application designed to help users quickly capture, organize, and manage their memos efficiently. The application provides a clean, intuitive interface with advanced features for categorizing, searching, and sorting notes.

### Problem It Solves
In today's fast-paced world, people need a quick and efficient way to jot down important information. Fast Memo addresses this need by providing:
- **Quick Note Capture**: Users can instantly create memos without complex navigation
- **Organization**: Notes can be categorized into predefined categories (Classes, Lecture Notes, Assignments, Exams & Tests, To-Do, Reminders, Personal)
- **Search Functionality**: Powerful search to find memos by title or content
- **Data Security**: PIN-based security to protect sensitive notes
- **Modern UI**: Dark theme interface with Material Design 3 components

### Target Users
- **Students**: For taking class notes, managing assignments, and organizing study materials
- **Professionals**: For quick task management and reminders
- **General Users**: Anyone who needs a simple, efficient note-taking solution

---

## 2. Technology Stack

### Programming Language
- **Java** - The entire application is developed using Java programming language (Java 11)

### Android SDK Version
- **Minimum SDK**: 21 (Android 5.0 Lollipop)
- **Target SDK**: 36 (Latest Android version)
- **Compile SDK**: 36

### Libraries and Dependencies

#### Core Android Libraries
- **AppCompat** (1.7.1) - Provides backward compatibility for newer Android features
- **Material Components** (1.13.0) - Material Design 3 UI components (Chips, TextFields, Cards, Buttons)
- **Activity** (1.8.2) - Modern Activity APIs and edge-to-edge support
- **ConstraintLayout** (2.2.1) - Flexible layout system
- **RecyclerView** (1.3.2) - Efficient list rendering for memo items

#### Architecture Components
- **Room Database** (2.6.1) - SQLite database abstraction layer
  - `room-runtime` - Runtime library
  - `room-compiler` - Annotation processor for generating database code
- **Lifecycle Components** (2.7.0) - Lifecycle-aware components
  - `lifecycle-viewmodel` - ViewModel for data management
  - `lifecycle-livedata` - Observable data holders
  - `lifecycle-runtime` - Runtime for lifecycle components

#### Security
- **Security Crypto** (1.1.0-alpha06) - Encrypted SharedPreferences for secure PIN storage

#### Testing
- **JUnit** (4.13.2) - Unit testing framework
- **Espresso** (3.7.0) - UI testing framework
- **AndroidX Test JUnit** (1.3.0) - Android JUnit extensions

### Architecture Pattern
The application follows **MVVM (Model-View-ViewModel)** architecture pattern:

- **Model**: `Memo.java` (Entity), `MemoDatabase.java`, `MemoDao.java`
- **View**: Activities (`MainActivity`, `MemoEditorActivity`, `MemoDetailsActivity`, `SplashActivity`) and Layout XML files
- **ViewModel**: `MemoViewModel.java` - Manages UI-related data and handles communication between View and Model
- **Repository**: `MemoRepository.java` - Single source of truth for data, abstracts data sources

---

## 3. Project File Structure

### Complete Directory Structure

```
noteMemo/
│
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/example/notememo/
│   │   │   │   ├── MainActivity.java          # Main screen with memo list
│   │   │   │   ├── MemoEditorActivity.java    # Create/Edit memo screen
│   │   │   │   ├── MemoDetailsActivity.java   # View memo details screen
│   │   │   │   ├── SplashActivity.java        # Splash/launch screen
│   │   │   │   ├── MemoAdapter.java           # RecyclerView adapter for memo list
│   │   │   │   ├── Memo.java                  # Entity/Model class
│   │   │   │   ├── MemoDatabase.java          # Room database class
│   │   │   │   ├── MemoDao.java               # Data Access Object interface
│   │   │   │   ├── MemoRepository.java        # Repository pattern implementation
│   │   │   │   ├── MemoViewModel.java         # ViewModel for data management
│   │   │   │   └── SecurityHelper.java        # PIN security utility
│   │   │   │
│   │   │   ├── res/
│   │   │   │   ├── layout/
│   │   │   │   │   ├── activity_main.xml           # Main activity layout
│   │   │   │   │   ├── activity_memo_editor.xml    # New memo editor layout
│   │   │   │   │   ├── activity_memo_editor_edit.xml  # Edit memo layout
│   │   │   │   │   ├── activity_memo_details.xml   # Memo details layout
│   │   │   │   │   ├── activity_splash.xml         # Splash screen layout
│   │   │   │   │   ├── item_memo.xml              # RecyclerView item layout
│   │   │   │   │   └── empty_search_state.xml     # Empty search state layout
│   │   │   │   │
│   │   │   │   ├── menu/
│   │   │   │   │   ├── main_menu.xml          # Main activity menu
│   │   │   │   │   ├── toolbar_main.xml       # Editor toolbar menu
│   │   │   │   │   └── toolbar_details.xml    # Details toolbar menu
│   │   │   │   │
│   │   │   │   ├── values/
│   │   │   │   │   ├── strings.xml            # String resources
│   │   │   │   │   ├── colors.xml             # Color resources
│   │   │   │   │   └── themes.xml             # App themes
│   │   │   │   │
│   │   │   │   ├── drawable/                  # Drawable resources
│   │   │   │   ├── mipmap/                    # App icons
│   │   │   │   └── xml/                       # XML configuration files
│   │   │   │
│   │   │   └── AndroidManifest.xml            # App manifest
│   │   │
│   │   ├── test/                              # Unit tests
│   │   └── androidTest/                       # Instrumented tests
│   │
│   └── build.gradle.kts                      # App-level Gradle configuration
│
├── build.gradle.kts                          # Project-level Gradle configuration
├── settings.gradle.kts                       # Project settings
├── gradle.properties                         # Gradle properties
└── gradle/                                   # Gradle wrapper files
```

### Purpose of Each Folder

#### `app/src/main/java/com/example/notememo/`
Contains all Java source code files:
- **Activities**: User interface controllers that manage screens
- **Adapters**: Bridge between data and RecyclerView
- **Models**: Data structure definitions
- **Database**: Room database setup and data access objects
- **Repository**: Data abstraction layer
- **ViewModel**: UI-related data management
- **Utilities**: Helper classes for security and other utilities

#### `app/src/main/res/layout/`
Contains XML layout files that define the visual structure of each screen:
- Activity layouts define the overall screen structure
- Item layouts define individual list item appearance
- Includes reusable layout components

#### `app/src/main/res/menu/`
Contains menu resource files that define toolbar and context menus for different activities.

#### `app/src/main/res/values/`
Contains resource definitions:
- `strings.xml`: All text strings used in the app
- `colors.xml`: Color definitions for theming
- `themes.xml`: App theme definitions

#### `app/src/main/res/drawable/`
Contains drawable resources like icons and images.

#### `app/src/main/res/mipmap/`
Contains application launcher icons in different densities.

### Important Files Explained

#### Activities

1. **SplashActivity.java**
   - **Purpose**: First screen shown when app launches
   - **Functionality**: Displays splash screen for 2 seconds, then navigates to MainActivity
   - **Contribution**: Provides smooth app launch experience

2. **MainActivity.java**
   - **Purpose**: Main screen showing list of all memos
   - **Functionality**: 
     - Displays memo list in RecyclerView
     - Search functionality
     - Category filtering via chips
     - Sorting options
     - PIN security check
     - Navigation to editor and details screens
   - **Contribution**: Central hub for memo management

3. **MemoEditorActivity.java**
   - **Purpose**: Screen for creating new memos or editing existing ones
   - **Functionality**: 
     - Input fields for title and content
     - Category selection
     - Save/cancel operations
   - **Contribution**: Enables memo creation and modification

4. **MemoDetailsActivity.java**
   - **Purpose**: Screen for viewing full memo details
   - **Functionality**: 
     - Displays complete memo information
     - Edit and delete options
     - Metadata display (creation and update timestamps)
   - **Contribution**: Provides detailed memo view

#### Adapters

**MemoAdapter.java**
- **Purpose**: Connects memo data to RecyclerView for display
- **Functionality**: 
  - Binds memo objects to list items
  - Handles click and long-press events
  - Formats timestamps for display
  - Applies category colors
- **Contribution**: Efficiently displays memo list with optimized updates using DiffUtil

#### Models

**Memo.java**
- **Purpose**: Data model representing a single memo
- **Functionality**: 
  - Stores memo properties (title, content, category, timestamps)
  - Provides getters and setters
  - Room entity with database annotations
- **Contribution**: Defines data structure used throughout the app

#### Database Classes

1. **MemoDatabase.java**
   - **Purpose**: Room database singleton instance
   - **Functionality**: 
     - Creates database instance
     - Provides access to DAO
     - Handles database versioning
   - **Contribution**: Manages SQLite database lifecycle

2. **MemoDao.java**
   - **Purpose**: Data Access Object interface for database operations
   - **Functionality**: 
     - Defines SQL queries for CRUD operations
     - Provides search and sorting queries
     - Returns LiveData for reactive updates
   - **Contribution**: Abstracts database operations from business logic

#### Repository

**MemoRepository.java**
- **Purpose**: Single source of truth for memo data
- **Functionality**: 
  - Encapsulates data access logic
  - Handles sorting modes
  - Executes database operations on background threads
- **Contribution**: Separates data access from ViewModel, enables testing

#### ViewModel

**MemoViewModel.java**
- **Purpose**: Manages UI-related data and survives configuration changes
- **Functionality**: 
  - Holds search query, category filter, and sort mode
  - Combines filters using MediatorLiveData
  - Provides memo list to UI
- **Contribution**: Keeps UI data separate from Activity, enables data persistence across screen rotations

#### Utilities

**SecurityHelper.java**
- **Purpose**: Manages PIN-based security
- **Functionality**: 
  - Stores and verifies PIN using encrypted SharedPreferences
  - Hashes PIN using SHA-256
  - Manages PIN enable/disable state
- **Contribution**: Provides app-level security for protecting sensitive notes

---

## 4. Application Workflow

### App Launch Flow

1. **SplashActivity** (Launcher Activity)
   - App starts → `SplashActivity` is displayed
   - Shows splash screen for 2 seconds (`SPLASH_DURATION = 2000ms`)
   - After delay, creates Intent to navigate to `MainActivity`
   - Calls `finish()` to remove splash from back stack

2. **MainActivity** - PIN Check
   - `onCreate()` checks if PIN is enabled via `SecurityHelper.isPinEnabled()`
   - If PIN enabled:
     - Shows PIN dialog immediately
     - Blocks UI until correct PIN is entered
     - On correct PIN: Proceeds with normal initialization
     - On incorrect PIN: Shows toast and finishes activity
   - If PIN not enabled: Proceeds directly to main screen

3. **MainActivity** - Initialization
   - Sets up EdgeToEdge for modern Android appearance
   - Initializes ViewModel
   - Sets up RecyclerView with MemoAdapter
   - Configures search functionality
   - Sets up category filter chips
   - Observes ViewModel LiveData for memo list updates

### Navigation Flow

```
SplashActivity
    ↓
MainActivity (List View)
    ├─→ MemoEditorActivity (New Memo)
    │       └─→ Back to MainActivity
    │
    ├─→ MemoDetailsActivity (View Memo)
    │       ├─→ MemoEditorActivity (Edit)
    │       │       └─→ Back to MemoDetailsActivity or MainActivity
    │       │
    │       └─→ Delete → Back to MainActivity
    │
    └─→ Search/Filter → Updates list in MainActivity
```

### User Interaction Flow

#### Creating a New Memo
1. User taps FloatingActionButton in MainActivity
2. Intent created to launch MemoEditorActivity
3. User enters title, content, and selects category
4. User taps Save button in toolbar
5. MemoEditorActivity creates new Memo object
6. Calls `viewModel.insert(memo)`
7. Repository executes insert on background thread
8. Database updates trigger LiveData update
9. MainActivity observes change and refreshes list
10. Editor activity finishes, returns to MainActivity

#### Viewing Memo Details
1. User taps a memo item in RecyclerView
2. MemoAdapter triggers click listener
3. Intent created with memo UID extra
4. MemoDetailsActivity receives intent
5. Activity observes `viewModel.getMemoById(uid)` LiveData
6. When memo loads, displays all details
7. User can edit (navigate to MemoEditorActivity) or delete

#### Editing a Memo
1. User taps Edit button in MemoDetailsActivity or long-presses item in MainActivity
2. Intent created with memo UID to MemoEditorActivity
3. MemoEditorActivity loads existing memo data
4. Pre-fills input fields with current values
5. User modifies content
6. On save, updates existing memo object
7. Calls `viewModel.update(memo)`
8. Repository updates database
9. LiveData updates trigger UI refresh in all observing activities

#### Deleting a Memo
1. User long-presses memo in MainActivity OR taps Delete in MemoDetailsActivity
2. Confirmation dialog appears
3. On confirmation, calls `viewModel.delete(memo)`
4. Repository executes delete on background thread
5. Database updates trigger LiveData update
6. List refreshes automatically
7. If in DetailsActivity, finishes and returns to MainActivity

#### Searching Memos
1. User types in search field
2. TextWatcher detects text changes
3. Updates `viewModel.setSearchQuery(query)`
4. ViewModel triggers `updateMemoList()`
5. Repository queries database with search string
6. Results update via LiveData
7. Adapter updates RecyclerView with filtered results

#### Filtering by Category
1. User taps category chip (Classes, Lecture Notes, etc.)
2. Chip listener updates `viewModel.setSelectedCategory(category)`
3. ViewModel triggers `updateMemoList()`
4. Repository queries memos by category
5. Results update via LiveData
6. Adapter updates RecyclerView with filtered results

#### Sorting Memos
1. User taps menu → Sort option
2. Selects sort mode (Newest First, Oldest First, By Category)
3. Updates `viewModel.setSortMode(mode)`
4. ViewModel triggers `updateMemoList()`
5. Repository queries with appropriate sort order
6. Results update via LiveData
7. Adapter updates RecyclerView with sorted results

### Data Flow Between Components

```
User Action (UI)
    ↓
Activity/Adapter
    ↓
ViewModel (setSearchQuery/setSelectedCategory/setSortMode)
    ↓
MemoViewModel.updateMemoList()
    ↓
MemoRepository.searchMemos(query, category, sortMode)
    ↓
MemoDao (Database Query)
    ↓
SQLite Database
    ↓
LiveData<List<Memo>> (Reactive Update)
    ↓
ViewModel.memoList (MediatorLiveData)
    ↓
Activity.observe() → Adapter.updateMemos()
    ↓
RecyclerView (UI Update)
```

---

## 5. Core Logic Explanation

### Detailed Logic in Each Java File

#### 5.1 SplashActivity.java

**Purpose**: Displays a splash screen when the app launches.

**Key Logic**:

1. **onCreate() Method**:
   - Enables EdgeToEdge for modern Android full-screen appearance
   - Sets content view to `activity_splash` layout
   - Configures window insets to handle system bars properly
   - Creates a Handler with MainLooper to schedule delayed navigation
   - Uses `postDelayed()` to wait 2 seconds (`SPLASH_DURATION`)
   - After delay, creates Intent to start MainActivity
   - Calls `finish()` to remove SplashActivity from back stack

**Why this approach**: Provides smooth app launch experience and ensures MainActivity starts after splash animation completes.

---

#### 5.2 MainActivity.java

**Purpose**: Main screen displaying list of memos with search, filter, and sort capabilities.

**Key Logic**:

1. **onCreate() Method**:
   - **PIN Security Check**: 
     - Checks if PIN is enabled using `SecurityHelper.isPinEnabled(this)`
     - If enabled, shows PIN dialog and returns early
     - If not enabled, proceeds with normal initialization
   - **EdgeToEdge Setup**: Enables modern full-screen mode
   - **ViewModel Initialization**: Creates MemoViewModel instance using AndroidViewModelFactory
   - **UI Setup**: Calls initialization methods for views, toolbar, RecyclerView, search, category filters, and FAB
   - **LiveData Observation**: Sets up observers to react to data changes

2. **showPinDialog() Method**:
   - Creates MaterialAlertDialogBuilder for PIN entry
   - Adds TextInputLayout with number password input type
   - Sets dialog properties (dim amount, blur effect)
   - On OK button click:
     - Retrieves PIN from input
     - Verifies PIN using `SecurityHelper.verifyPin()`
     - If correct: Initializes all UI components
     - If incorrect: Shows toast and finishes activity
   - On Cancel: Finishes activity

3. **setupRecyclerView() Method**:
   - Creates MemoAdapter with click listener that navigates to MemoDetailsActivity
   - Sets long-click listener that shows delete confirmation dialog
   - Configures LinearLayoutManager for vertical list
   - Attaches adapter to RecyclerView

4. **setupSearch() Method**:
   - Adds TextWatcher to search input field
   - **onTextChanged()**: 
     - Gets current text as query string
     - Updates ViewModel search query: `viewModel.setSearchQuery(query)`
     - Shows/hides clear button based on whether query is empty
   - ViewModel automatically triggers database query update via LiveData

5. **setupCategoryFilters() Method**:
   - Creates OnCheckedChangeListener for category chips
   - **When chip checked**:
     - If "All" chip: Unchecks all other chips, sets category to "All"
     - If specific category chip: Unchecks "All" and other chips, sets category
     - Applies category-specific background color to selected chip
   - **When chip unchecked**: Resets background color
   - Updates ViewModel category: `viewModel.setSelectedCategory(category)`

6. **observeViewModel() Method**:
   - Observes `viewModel.getMemoList()` LiveData
   - When memo list changes:
     - Updates adapter: `adapter.updateMemos(memos)`
     - Updates empty state UI: `updateEmptyState(memos)`

7. **updateEmptyState() Method**:
   - Checks if search query exists and is not empty
   - **If memos empty**:
     - If searching: Shows empty search state with message
     - If not searching: Shows "no memos" empty state
   - **If memos not empty**: Hides all empty states, shows RecyclerView

8. **showDeleteConfirmation() Method**:
   - Creates MaterialAlertDialogBuilder for delete confirmation
   - Shows memo title in confirmation message
   - On Delete: Calls `viewModel.delete(memo)` to remove from database
   - On Cancel: Dismisses dialog

9. **Menu Handling (onOptionsItemSelected)**:
   - **Sort Options**: Updates ViewModel sort mode (date desc, date asc, category)
   - **PIN Settings**: Shows PIN settings dialog with options to enable/disable/change PIN

**Why this approach**: 
- PIN check in onCreate ensures security before any UI is shown
- Reactive programming with LiveData ensures UI always reflects current data
- Separation of concerns: Activity handles UI, ViewModel handles data

---

#### 5.3 MemoEditorActivity.java

**Purpose**: Screen for creating new memos or editing existing memos.

**Key Logic**:

1. **onCreate() Method**:
   - Checks if editing existing memo by checking for `memo_uid` extra in Intent
   - **If editing** (`currentMemoUid != -1`):
     - Sets `isEditMode = true`
     - Loads `activity_memo_editor_edit` layout (has category chips)
   - **If creating new**:
     - Loads `activity_memo_editor` layout (has dropdown for category)
   - Initializes ViewModel
   - Sets up toolbar and views
   - If editing, loads existing memo data

2. **initViews() Method**:
   - Gets references to title, content, and category input fields
   - **For new memo mode**:
     - Sets up AutoCompleteTextView with category options array
     - Creates ArrayAdapter for dropdown suggestions
   - **For edit mode**:
     - Gets references to category chips
     - Sets up chip listeners via `setupCategoryChips()`

3. **setupCategoryChips() Method**:
   - Creates OnCheckedChangeListener for category chips
   - **When chip checked**:
     - Unchecks all other chips
     - Sets `selectedCategory` variable to selected category
     - Applies red background color to selected chip
   - **When chip unchecked**: Resets background color

4. **loadMemoData() Method**:
   - Observes `viewModel.getMemoById(currentMemoUid)` LiveData
   - When memo loads:
     - Pre-fills title and content fields with existing values
     - **If edit mode**: 
       - Checks appropriate category chip based on memo's category
       - Updates "Last Edited" timestamp display
     - **If new mode**: Sets category dropdown to memo's category

5. **saveMemo() Method**:
   - Retrieves title, content, and category from input fields
   - **If editing**:
     - Observes memo from database
     - Updates memo object's fields
     - Calls `viewModel.update(memo)` to save changes
   - **If creating new**:
     - Creates new Memo object with constructor
     - Calls `viewModel.insert(newMemo)` to save
   - Finishes activity to return to previous screen

6. **onOptionsItemSelected() Method**:
   - **Home/Back button**: Finishes activity (cancels without saving)
   - **Save button**: Calls `saveMemo()` to persist changes

**Why this approach**:
- Single activity handles both create and edit modes for code reusability
- Different layouts for create vs edit provide appropriate UI (dropdown vs chips)
- ViewModel ensures data is saved correctly to database
- Finishing activity triggers automatic LiveData updates in MainActivity

---

#### 5.4 MemoDetailsActivity.java

**Purpose**: Displays full details of a selected memo.

**Key Logic**:

1. **onCreate() Method**:
   - Retrieves memo UID from Intent extras
   - Supports both `memo_uid` (int) and `memo_id` (string) for backward compatibility
   - If no UID found, finishes activity immediately
   - Initializes ViewModel and sets up toolbar and views
   - Loads memo data from database

2. **loadMemoData() Method**:
   - Observes `viewModel.getMemoById(memoUid)` LiveData
   - When memo loads:
     - Displays title, content, category in UI
     - Formats creation timestamp using SimpleDateFormat
     - Calculates time difference for "Updated" timestamp:
       - If updated less than 1 minute ago: Shows "Updated just now"
       - Otherwise: Shows formatted date/time
     - Applies category-specific color to category chip
   - If memo is null (deleted), finishes activity

3. **showDeleteConfirmation() Method**:
   - Observes memo to get current data
   - **Important**: Removes observer after first callback to prevent multiple calls
   - Shows confirmation dialog with memo title
   - On Delete: Calls `viewModel.delete(memo)` and finishes activity
   - On Cancel: Dismisses dialog

4. **onOptionsItemSelected() Method**:
   - **Home/Back button**: Finishes activity, returns to MainActivity
   - **Edit button**: Creates Intent to MemoEditorActivity with memo UID, starts activity
   - **Delete button**: Shows delete confirmation dialog

5. **getCategoryColor() Method**:
   - Maps category names to color resources
   - Returns appropriate color for category chip background

**Why this approach**:
- Observer pattern ensures UI updates if memo changes while viewing
- Removing observer after delete confirmation prevents memory leaks
- Formatting timestamps provides user-friendly relative time display

---

#### 5.5 MemoAdapter.java

**Purpose**: Binds memo data to RecyclerView items for display.

**Key Logic**:

1. **Constructor**:
   - Takes OnMemoClickListener interface for handling item clicks
   - Initializes empty list for memos

2. **onCreateViewHolder() Method**:
   - Inflates `item_memo.xml` layout for each list item
   - Returns MemoViewHolder instance

3. **onBindViewHolder() Method**:
   - Gets memo at position
   - Calls `holder.bind(memo)` to populate views with data

4. **updateMemos() Method**:
   - **Efficient Update Logic**:
     - If memos list is null (first load): Sets list and notifies all items inserted
     - Otherwise: Uses DiffUtil to calculate differences between old and new lists
     - DiffUtil compares items by UID (areItemsTheSame) and content (areContentsTheSame)
     - Only updates changed items, not entire list (performance optimization)

5. **MemoDiffCallback Inner Class**:
   - Implements DiffUtil.Callback interface
   - **getOldListSize() / getNewListSize()**: Returns list sizes for comparison
   - **areItemsTheSame()**: Compares items by UID to determine if same item
   - **areContentsTheSame()**: Compares title, content, category, and updatedAt timestamp
   - **getChangePayload()**: Optional - could provide change details for partial updates

6. **MemoViewHolder Inner Class**:
   - **Constructor**: Gets references to all views in item layout
   - Sets up click listeners:
     - **onClick**: Triggers OnMemoClickListener to navigate to details
     - **onLongClick**: Triggers OnMemoLongClickListener to show delete dialog
   - **bind() Method**:
     - Sets title, content, category text
     - Applies category-specific color to chip
     - Formats timestamp using `formatTimestamp()` helper
     - Hides mic icon (reserved for future voice memo feature)

7. **formatTimestamp() Method**:
   - **Relative Time Formatting**:
     - Calculates time difference from now
     - If more than 1 day ago: Shows "Yesterday", "X days ago", or date (MMM dd)
     - If more than 1 hour ago: Shows "X hour(s) ago"
     - If more than 1 minute ago: Shows "X minute(s) ago"
     - Otherwise: Shows "Just now"
   - Provides user-friendly time display instead of raw timestamps

8. **getCategoryColor() Method**:
   - Maps category string to color resource ID
   - Returns appropriate color for each category type

**Why this approach**:
- DiffUtil minimizes RecyclerView updates for better performance
- ViewHolder pattern reuses views for memory efficiency
- Relative time formatting improves user experience
- Separation of click handlers allows flexible navigation

---

#### 5.6 Memo.java

**Purpose**: Data model representing a memo entity.

**Key Logic**:

1. **Entity Annotations**:
   - `@Entity(tableName = "memo_table")`: Marks class as Room entity with table name
   - `@PrimaryKey(autoGenerate = true)`: UID is auto-generated primary key
   - `@ColumnInfo(name = "...")`: Maps fields to database columns

2. **Fields**:
   - `uid`: Integer primary key (auto-generated)
   - `title`: String memo title
   - `content`: String memo content
   - `category`: String category name
   - `createdAt`: Long timestamp (milliseconds since epoch)
   - `updatedAt`: Long timestamp (milliseconds since epoch)

3. **Constructors**:
   - **Default constructor**: Required by Room, sets timestamps to current time
   - **Parameterized constructor** (`@Ignore`): Convenience constructor for creating new memos
     - Calls default constructor to set timestamps
     - Sets title, content, category from parameters

4. **Getters and Setters**:
   - Standard getter/setter methods for all fields
   - Room uses these for database mapping

5. **Helper Methods**:
   - `getCreatedAtDate()`: Converts long timestamp to Date object
   - `getUpdatedAtDate()`: Converts long timestamp to Date object
   - Provides compatibility for code expecting Date objects

**Why this approach**:
- Room annotations simplify database mapping
- Long timestamps provide precise time tracking
- Auto-generated UID ensures unique identifiers
- Getters/setters enable Room to map data correctly

---

#### 5.7 MemoDatabase.java

**Purpose**: Room database singleton instance.

**Key Logic**:

1. **Database Annotation**:
   - `@Database(entities = {Memo.class}, version = 1, exportSchema = false)`
   - Declares Memo as the only entity
   - Version 1 indicates first database schema version
   - `exportSchema = false` disables schema export (simplifies build)

2. **Abstract DAO Method**:
   - `public abstract MemoDao memoDao()`: Room generates implementation
   - Provides access to database operations

3. **Singleton Pattern**:
   - **INSTANCE**: Volatile static field to hold database instance
   - **getDatabase() Method**:
     - **Double-Checked Locking**:
       - First null check (avoid synchronization if already initialized)
       - Synchronized block for thread safety
       - Second null check inside synchronized block (prevent multiple instances)
     - **Database Builder**:
       - Uses `Room.databaseBuilder()` with context, class, and database name
       - `fallbackToDestructiveMigration()`: Drops and recreates database on schema change
       - Builds and returns database instance

**Why this approach**:
- Singleton ensures only one database instance exists (memory efficiency)
- Double-checked locking provides thread safety without unnecessary synchronization
- Room handles SQLite database creation and management automatically
- Fallback to destructive migration simplifies development (in production, would use proper migrations)

---

#### 5.8 MemoDao.java

**Purpose**: Data Access Object interface defining database queries.

**Key Logic**:

1. **CRUD Operations**:
   - `@Insert(onConflict = OnConflictStrategy.REPLACE)`: Inserts memo, replaces on conflict
   - `@Update(onConflict = OnConflictStrategy.REPLACE)`: Updates memo, replaces on conflict
   - `@Delete`: Deletes memo from database

2. **Query Operations with LiveData**:
   - All query methods return `LiveData<List<Memo>>` or `LiveData<Memo>`
   - LiveData ensures reactive updates when database changes

3. **Basic Queries**:
   - `getAllMemos()`: Returns all memos sorted by `updated_at DESC` (newest first)
   - `getMemoById(uid)`: Returns single memo by UID

4. **Category Filtering Queries**:
   - `getMemosByCategory(category)`: Filters by category, sorted by `updated_at DESC`
   - `getMemosByCategorySortedByCreatedAsc(category)`: Same filter, sorted by `created_at ASC`

5. **Search Queries**:
   - Uses SQL `LIKE` operator with pattern matching
   - Pattern: `'%' || :query || '%'` searches for query anywhere in title or content
   - Multiple search queries support different sorting modes:
     - `searchMemos(query)`: Default sort (updated_at DESC)
     - `searchMemosSortedByCreatedAsc(query)`: Sort by created_at ASC
     - `searchMemosSortedByCategory(query)`: Sort by category ASC, then updated_at DESC

6. **Combined Search and Category Queries**:
   - `searchMemosByCategory(query, category)`: Searches within specific category
   - Supports same sorting variations as regular search

7. **Sorting Queries**:
   - `getAllMemosSortedByCreatedDesc()`: All memos, newest created first
   - `getAllMemosSortedByCreatedAsc()`: All memos, oldest created first
   - `getAllMemosSortedByCategory()`: All memos, sorted by category then updated date

**Why this approach**:
- Separate queries for each combination avoids complex dynamic SQL generation
- LiveData provides reactive updates without manual observation
- SQL LIKE pattern matching enables flexible text search
- Multiple sort queries support different UI sorting modes

---

#### 5.9 MemoRepository.java

**Purpose**: Repository pattern implementation - single source of truth for data.

**Key Logic**:

1. **Initialization**:
   - Constructor takes Application context
   - Gets database instance: `MemoDatabase.getDatabase(application)`
   - Gets DAO from database: `db.memoDao()`
   - Creates ExecutorService with 2 threads for background database operations

2. **Sort Mode Constants**:
   - `SORT_BY_DATE_DESC = 0`: Newest first (default)
   - `SORT_BY_DATE_ASC = 1`: Oldest first
   - `SORT_BY_CATEGORY = 2`: Sort by category

3. **getAllMemos(sortMode) Method**:
   - **Switch statement** based on sort mode:
     - `SORT_BY_DATE_ASC`: Calls `memoDao.getAllMemosSortedByCreatedAsc()`
     - `SORT_BY_CATEGORY`: Calls `memoDao.getAllMemosSortedByCategory()`
     - Default (`SORT_BY_DATE_DESC`): Calls `memoDao.getAllMemos()`
   - Returns appropriate LiveData based on sort mode

4. **getMemosByCategory(category, sortMode) Method**:
   - If category is null or "All": Delegates to `getAllMemos(sortMode)`
   - Otherwise, switches on sort mode:
     - `SORT_BY_DATE_ASC`: Calls `memoDao.getMemosByCategorySortedByCreatedAsc(category)`
     - `SORT_BY_CATEGORY`: Calls `memoDao.getMemosByCategory(category)` (already sorted by date within category)
     - Default: Calls `memoDao.getMemosByCategory(category)`
   - Returns filtered and sorted LiveData

5. **searchMemos(query, category, sortMode) Method**:
   - **Multi-level filtering logic**:
     - If query is empty: Delegates to `getMemosByCategory(category, sortMode)`
     - If category is not "All": Searches within category with sorting
     - Otherwise: Searches all memos with sorting
   - **Switch statements** determine which DAO method to call based on:
     - Whether category filter is applied
     - Sort mode selected
   - Returns LiveData with search results

6. **getMemoById(uid) Method**:
   - Directly delegates to `memoDao.getMemoById(uid)`
   - Returns LiveData for single memo

7. **insert(memo) Method**:
   - **Background Execution**: 
     - Executes on executor thread (not main thread)
     - Sets `updatedAt` timestamp to current time
     - Calls `memoDao.insert(memo)`
   - **Why background**: Room database operations should not block UI thread

8. **update(memo) Method**:
   - **Background Execution**:
     - Executes on executor thread
     - Sets `updatedAt` timestamp to current time (tracks modification)
     - Calls `memoDao.update(memo)`

9. **delete(memo) Method**:
   - **Background Execution**:
     - Executes on executor thread
     - Calls `memoDao.delete(memo)`

**Why this approach**:
- Repository pattern abstracts data source (could be database, network, etc.)
- Background execution prevents blocking UI thread during database operations
- Automatic timestamp updates ensure `updatedAt` always reflects last modification
- Switch-based routing provides clear, maintainable query selection logic

---

#### 5.10 MemoViewModel.java

**Purpose**: ViewModel manages UI-related data and survives configuration changes.

**Key Logic**:

1. **Initialization**:
   - Extends `AndroidViewModel` (has Application reference)
   - Constructor takes Application context
   - Creates MemoRepository instance
   - Initializes MutableLiveData for search query, selected category, and sort mode
   - Creates MediatorLiveData for memo list

2. **MutableLiveData Fields**:
   - `searchQuery`: Holds current search text (default: empty string)
   - `selectedCategory`: Holds selected category filter (default: "All")
   - `sortMode`: Holds current sort mode (default: `SORT_BY_DATE_DESC`)

3. **MediatorLiveData Pattern**:
   - `memoList`: MediatorLiveData that combines multiple data sources
   - **addSource()**: Observes searchQuery, selectedCategory, and sortMode
   - When any source changes, triggers `updateMemoList()` method

4. **updateMemoList() Method**:
   - **Reactive Update Logic**:
     - Gets current values from searchQuery, selectedCategory, sortMode
     - Removes previous LiveData source from MediatorLiveData (prevents duplicate updates)
     - Calls `repository.searchMemos(query, category, sort)` to get new LiveData
     - Adds new LiveData as source to MediatorLiveData
     - Observer callback updates MediatorLiveData value when repository data changes
   - **Why MediatorLiveData**: Combines multiple LiveData sources (search + category + sort) into single observable

5. **Getter Methods**:
   - `getMemoList()`: Returns MediatorLiveData for UI observation
   - `getSearchQuery()`, `getSelectedCategory()`, `getSortMode()`: Return MutableLiveData for observation

6. **Setter Methods**:
   - `setSearchQuery(query)`: Updates search query, triggers `updateMemoList()` via observer
   - `setSelectedCategory(category)`: Updates category filter, triggers `updateMemoList()` via observer
   - `setSortMode(mode)`: Updates sort mode, triggers `updateMemoList()` via observer
   - All setters handle null values by providing defaults

7. **CRUD Methods**:
   - `insert(memo)`: Delegates to repository
   - `update(memo)`: Delegates to repository
   - `delete(memo)`: Delegates to repository
   - `getMemoById(uid)`: Delegates to repository, returns LiveData

**Why this approach**:
- ViewModel survives configuration changes (screen rotation) - data persists
- MediatorLiveData combines multiple filters into single observable list
- Reactive programming: UI automatically updates when data changes
- Separation of concerns: ViewModel handles data, Activity handles UI

---

#### 5.11 SecurityHelper.java

**Purpose**: Manages PIN-based security using encrypted storage.

**Key Logic**:

1. **Constants**:
   - `PREFS_NAME`: SharedPreferences file name for security data
   - `KEY_PIN_ENABLED`: Boolean key for PIN enabled state
   - `KEY_PIN_HASH`: String key for hashed PIN value

2. **isPinEnabled(context) Method**:
   - Gets SharedPreferences instance
   - Reads `KEY_PIN_ENABLED` boolean value
   - Returns false if not set (default)

3. **setPinEnabled(context, enabled) Method**:
   - Gets SharedPreferences instance
   - Updates `KEY_PIN_ENABLED` boolean value
   - Uses `apply()` for asynchronous write (non-blocking)

4. **setPin(context, pin) Method**:
   - Hashes PIN using `hashPin(pin)` method
   - Stores hashed PIN in SharedPreferences
   - Enables PIN by setting `KEY_PIN_ENABLED` to true
   - **Why hash**: PIN is never stored in plain text for security

5. **verifyPin(context, pin) Method**:
   - Gets stored PIN hash from SharedPreferences
   - Hashes input PIN using same algorithm
   - Compares stored hash with input hash
   - Returns true if hashes match (PIN correct), false otherwise
   - **Why hash comparison**: Never compares plain text PINs

6. **hashPin(pin) Private Method**:
   - **SHA-256 Hashing**:
     - Gets MessageDigest instance with "SHA-256" algorithm
     - Converts PIN string to bytes using UTF-8 encoding
     - Computes hash digest
     - Converts byte array to hexadecimal string representation
     - Returns hash string
   - **Error Handling**: 
     - If hashing fails (exception), returns plain PIN as fallback
     - Not secure but prevents app crash

7. **getSharedPreferences(context) Private Method**:
   - **Encrypted SharedPreferences**:
     - Creates MasterKey using AES256_GCM scheme
     - Creates EncryptedSharedPreferences with:
       - Context and file name
       - MasterKey for encryption
       - AES256_SIV for key encryption
       - AES256_GCM for value encryption
   - **Fallback**:
     - If encryption fails (exception), falls back to regular SharedPreferences
     - Ensures app works even if encryption library has issues
     - Regular SharedPreferences still protects data (not encrypted but app-private)

**Why this approach**:
- SHA-256 hashing ensures PIN is never stored in plain text
- EncryptedSharedPreferences provides additional security layer
- Fallback to regular SharedPreferences ensures app functionality
- `apply()` instead of `commit()` prevents blocking UI thread

---

## 6. Database & Data Management

### Database Used
**Room Database** (abstraction over SQLite)

Room is Google's recommended database solution for Android, providing:
- Type-safe SQL queries
- Compile-time query verification
- Automatic entity-to-database mapping
- LiveData integration for reactive updates
- Background thread execution

### Database Schema

#### Table: `memo_table`

| Column Name | Data Type | Constraints | Description |
|------------|-----------|-------------|-------------|
| `uid` | INTEGER | PRIMARY KEY, AUTO_INCREMENT | Unique identifier for each memo |
| `title` | TEXT | | Memo title (can be null) |
| `content` | TEXT | | Memo content text |
| `category` | TEXT | | Category name (Classes, Lecture Notes, etc.) |
| `created_at` | INTEGER | | Timestamp when memo was created (milliseconds since epoch) |
| `updated_at` | INTEGER | | Timestamp when memo was last updated (milliseconds since epoch) |

### Entity: Memo Class

The `Memo` class is annotated with Room annotations to map to the database table:

```java
@Entity(tableName = "memo_table")
public class Memo {
    @PrimaryKey(autoGenerate = true)
    public int uid;
    
    @ColumnInfo(name = "title")
    public String title;
    
    // ... other fields
}
```

### CRUD Operations

#### Create (Insert)
- **Method**: `MemoDao.insert(Memo memo)`
- **Implementation**: `@Insert` annotation with `OnConflictStrategy.REPLACE`
- **Flow**: 
  1. User saves memo in MemoEditorActivity
  2. MemoViewModel.insert() → MemoRepository.insert()
  3. Repository executes on background thread
  4. Sets `updatedAt` timestamp
  5. DAO inserts into database
  6. LiveData automatically notifies observers

#### Read (Query)
- **Methods**: Multiple query methods in MemoDao
- **Implementation**: `@Query` annotations with SQL statements
- **Types**:
  - `getAllMemos()`: Returns all memos
  - `getMemoById(uid)`: Returns single memo
  - `getMemosByCategory(category)`: Filters by category
  - `searchMemos(query)`: Searches title/content
  - Sorting variations for each query type
- **Flow**:
  1. ViewModel requests data from Repository
  2. Repository calls appropriate DAO method
  3. DAO executes SQL query
  4. Returns LiveData<List<Memo>> or LiveData<Memo>
  5. Observers in Activities automatically receive updates

#### Update
- **Method**: `MemoDao.update(Memo memo)`
- **Implementation**: `@Update` annotation with `OnConflictStrategy.REPLACE`
- **Flow**:
  1. User edits memo in MemoEditorActivity
  2. MemoViewModel.update() → MemoRepository.update()
  3. Repository executes on background thread
  4. Sets `updatedAt` timestamp to current time
  5. DAO updates database row matching UID
  6. LiveData automatically notifies observers

#### Delete
- **Method**: `MemoDao.delete(Memo memo)`
- **Implementation**: `@Delete` annotation
- **Flow**:
  1. User confirms delete in MainActivity or MemoDetailsActivity
  2. MemoViewModel.delete() → MemoRepository.delete()
  3. Repository executes on background thread
  4. DAO deletes database row matching UID
  5. LiveData automatically notifies observers
  6. RecyclerView updates to reflect deletion

### Data Storage Details

#### Timestamps
- **Format**: Long integers (milliseconds since Unix epoch: January 1, 1970)
- **Created At**: Set when memo is first created (never changes)
- **Updated At**: Set when memo is created and updated whenever memo is modified
- **Usage**: Display relative time ("2 days ago") or formatted dates

#### Category Values
Predefined categories stored as strings:
- "Classes"
- "Lecture Notes"
- "Assignments"
- "Exams & Tests"
- "To-Do"
- "Reminders"
- "Personal"

### Data Retrieval and Filtering

#### Search Functionality
- **SQL Pattern**: `LIKE '%' || :query || '%'`
- **Fields Searched**: Title and Content
- **Case Sensitivity**: SQLite LIKE is case-insensitive by default
- **Implementation**: Multiple search queries support different sort modes

#### Category Filtering
- **Implementation**: SQL WHERE clause: `WHERE category = :category`
- **"All" Category**: Handled in Repository layer (returns all memos)

#### Sorting
Three sorting modes:
1. **Date Descending (Newest First)**: `ORDER BY updated_at DESC`
2. **Date Ascending (Oldest First)**: `ORDER BY created_at ASC`
3. **Category**: `ORDER BY category ASC, updated_at DESC`

#### Combined Filtering
Repository combines search query, category filter, and sort mode:
- If search query exists: Applies search filter
- If category != "All": Applies category filter
- Applies appropriate sort order
- All filters can be applied simultaneously

### Data Flow in Database Operations

```
UI Action
    ↓
ViewModel Method (insert/update/delete)
    ↓
Repository Method (background thread execution)
    ↓
DAO Method (annotated with @Insert/@Update/@Delete)
    ↓
Room Database (SQLite)
    ↓
Database Change Detected
    ↓
LiveData Observer Notification
    ↓
UI Update (RecyclerView refresh)
```

### Security and Data Protection

#### PIN Storage
- **Location**: EncryptedSharedPreferences (separate from Room database)
- **Encryption**: AES256_GCM for values, AES256_SIV for keys
- **PIN Format**: SHA-256 hash stored (never plain text)
- **File**: `fast_memo_security` SharedPreferences file

#### Database Security
- Database file stored in app's private directory (not accessible to other apps)
- No external database connection (local-only)
- Room provides SQL injection protection through parameterized queries

---

## 7. UI & UX Design

### Layout Files Explanation

#### activity_main.xml
**Purpose**: Main screen layout showing memo list with search and filters.

**Key Components**:
1. **CoordinatorLayout**: Root container enabling Material Design behaviors
2. **AppBarLayout + Toolbar**: Top app bar with menu options
3. **Search Container**: 
   - TextInputLayout with TextInputEditText for search input
   - Clear button (ImageButton) shown when text exists
4. **Category Chips Container**:
   - HorizontalScrollView for horizontal scrolling of chips
   - Multiple Material Chip components for category filtering
5. **RecyclerView**: 
   - Displays memo list
   - Uses item_memo.xml for each item layout
6. **Empty States**:
   - Empty state for no memos (centered icon and message)
   - Empty search state for no search results
   - Visibility toggled based on data state
7. **FloatingActionButton**: 
   - Red circular button at bottom-right
   - Opens MemoEditorActivity for new memo

**Design Features**:
- Dark theme colors (`background_dark`, `surface_dark`)
- Red accent color (`red_primary`) for FAB and active chips
- Material Design 3 components (Chips, TextFields, Cards)

#### activity_memo_editor.xml / activity_memo_editor_edit.xml
**Purpose**: Layouts for creating/editing memos.

**Key Components**:
1. **Toolbar**: App bar with back button and save action
2. **TextInputLayout + TextInputEditText**: 
   - Title input field
   - Content input field (multi-line)
3. **Category Selection**:
   - **New memo**: AutoCompleteTextView dropdown
   - **Edit mode**: Category chips (similar to MainActivity)
4. **Last Edited Indicator** (edit mode only): Shows timestamp of last modification

**Design Features**:
- EdgeToEdge layout for modern full-screen appearance
- Material TextFields with filled box style
- Consistent dark theme

#### activity_memo_details.xml
**Purpose**: Layout for viewing full memo details.

**Key Components**:
1. **Toolbar**: App bar with back, edit, and delete actions
2. **Title TextView**: Large, bold text for memo title
3. **Content TextView**: Full content display (scrollable)
4. **Category Chip**: Colored chip showing category
5. **Metadata Section**: 
   - Created timestamp
   - Updated timestamp with relative time

**Design Features**:
- Read-only display (no input fields)
- Clear typography hierarchy (title > content > metadata)
- Color-coded category chips

#### item_memo.xml
**Purpose**: Individual memo item layout for RecyclerView.

**Key Components**:
1. **MaterialCardView**: 
   - Rounded corners (12dp)
   - Dark surface color
   - Elevation for depth
2. **Title TextView**: Bold, primary text color
3. **Content Preview TextView**: 
   - Secondary text color
   - Max 2 lines with ellipsis
4. **Category Chip**: Small chip with category name
5. **Timestamp TextView**: Relative time display ("2 days ago")
6. **Mic Icon** (hidden): Reserved for future voice memo feature

**Design Features**:
- Card-based design for visual separation
- Compact layout for list efficiency
- Color-coded categories

#### activity_splash.xml
**Purpose**: Splash screen layout.

**Key Components**:
- Simple layout with app branding (typically logo/image)
- Full-screen appearance
- Smooth transition to main screen

### RecyclerView Usage

#### Implementation
- **Adapter**: `MemoAdapter` extends `RecyclerView.Adapter<MemoAdapter.MemoViewHolder>`
- **Layout Manager**: `LinearLayoutManager` (vertical list)
- **View Binding**: Uses `findViewById()` in ViewHolder (could be upgraded to View Binding)

#### Optimization Techniques

1. **DiffUtil**:
   - `MemoDiffCallback` compares old and new lists
   - Only updates changed items (not entire list)
   - Improves scroll performance

2. **ViewHolder Pattern**:
   - ViewHolder caches view references
   - Reuses views for different items
   - Reduces `findViewById()` calls

3. **LiveData Integration**:
   - Automatic updates when database changes
   - No manual list refreshing needed

### Adapter Logic

#### MemoAdapter Responsibilities
1. **Data Binding**: Populates views with memo data
2. **Event Handling**: Manages click and long-press events
3. **Formatting**: Formats timestamps for display
4. **Styling**: Applies category colors to chips

#### Efficient Updates
- `updateMemos()` method receives new list
- Uses DiffUtil to calculate minimal changes
- Notifies adapter of specific changes (not full refresh)
- Maintains smooth scrolling during updates

### View Binding vs findViewById

**Current Implementation**: Uses `findViewById()` in all activities and adapter.

**Potential Improvement**: Could use View Binding (enabled in build.gradle.kts):
- Type-safe view references
- Null safety
- Better IDE support
- However, current implementation works correctly

### Color Scheme

#### Theme Colors
- **Background Dark**: `#121212` (near black)
- **Surface Dark**: `#1E1E1E` (dark gray)
- **Surface Variant**: `#2A2A2A` (lighter dark gray)

#### Accent Colors
- **Red Primary**: `#FF4444` (bright red)
  - Used for: FAB, active "All" chip, category chips

#### Category Colors
- **Classes**: `#2196F3` (Blue)
- **Lecture Notes**: `#9C27B0` (Purple)
- **Assignments**: `#FF9800` (Orange)
- **Exams & Tests**: `#F44336` (Red)
- **To-Do**: `#4CAF50` (Green)
- **Reminders**: `#FFC107` (Yellow)
- **Personal**: `#FF4444` (Red, same as primary)

#### Text Colors
- **Primary Text**: `#FFFFFF` (White)
- **Secondary Text**: `#B3B3B3` (Light gray)
- **Hint Text**: `#666666` (Medium gray)

### User Experience Features

1. **Empty States**: 
   - Clear messaging when no memos exist
   - Action button to create first memo
   - Different message for empty search results

2. **Search Feedback**:
   - Clear button appears when searching
   - Real-time search results as user types
   - Empty state message shows search query

3. **Category Visual Feedback**:
   - Active chip changes color
   - Other chips deselect automatically
   - Clear visual indication of active filter

4. **Relative Time Display**:
   - "Just now", "2 hours ago" instead of exact timestamps
   - More user-friendly than raw dates

5. **Confirmation Dialogs**:
   - Delete confirmation prevents accidental deletions
   - Shows memo title in confirmation message

6. **PIN Security**:
   - Immediate PIN check on app launch
   - Clear PIN entry dialog
   - Settings menu for PIN management

---

## 8. Android Manifest & Permissions

### AndroidManifest.xml Structure

```xml
<manifest>
    <application>
        <activity SplashActivity />  <!-- LAUNCHER -->
        <activity MainActivity />
        <activity MemoEditorActivity />
        <activity MemoDetailsActivity />
    </application>
</manifest>
```

### Activity Declarations

#### SplashActivity
- **Exported**: `true` (can be launched by system launcher)
- **Intent Filter**: 
  - Action: `MAIN` (entry point)
  - Category: `LAUNCHER` (appears in app drawer)
- **Theme**: `Theme.NoteMemo` (custom app theme)

#### MainActivity
- **Exported**: `false` (only launched internally)
- **No Intent Filter**: Not directly accessible from outside app

#### MemoEditorActivity
- **Exported**: `false`
- **Parent Activity**: `MainActivity` (back navigation support)
- **No Intent Filter**: Launched programmatically with Intent

#### MemoDetailsActivity
- **Exported**: `false`
- **Parent Activity**: `MainActivity` (back navigation support)
- **No Intent Filter**: Launched programmatically with Intent

### Permissions Used

**No Permissions Required**: The app does not request any runtime permissions.

**Why No Permissions?**:
- **No Internet Access**: App works offline, no network operations
- **No Storage Access**: Uses Room database (app-private storage, no permission needed)
- **No Camera/Microphone**: No media capture features
- **No Location**: No location-based features
- **No Contacts**: No contact integration

### App Configuration

#### Application Tag Attributes
- **allowBackup**: `true` - Enables Android backup service
- **dataExtractionRules**: References XML rules for data backup
- **fullBackupContent**: References XML rules for full backup
- **icon**: App launcher icon
- **label**: App name ("Fast Memo")
- **roundIcon**: Round version of launcher icon
- **supportsRtl**: `true` - Supports right-to-left languages
- **theme**: Custom theme for app

### Security Considerations

1. **No Exported Activities** (except SplashActivity):
   - Prevents other apps from launching activities directly
   - Only SplashActivity is accessible from launcher

2. **Parent Activity Declaration**:
   - Enables proper back navigation
   - System can reconstruct navigation hierarchy

3. **App-Private Storage**:
   - Room database stored in app's private directory
   - Not accessible to other apps or users without root

4. **Encrypted SharedPreferences**:
   - PIN data stored securely using encryption
   - Even if device is compromised, PIN hash is encrypted

---

## 9. Build & Execution Process

### Gradle Configuration

#### Project-Level build.gradle.kts
```kotlin
plugins {
    alias(libs.plugins.android.application) apply false
}
```
- Applies Android application plugin (not to root project, only to app module)
- Version catalog reference for plugin version management

#### App-Level build.gradle.kts

**Configuration Details**:

1. **Namespace**: `com.example.notememo`
   - Package name for generated R class

2. **SDK Versions**:
   - **compileSdk**: 36 (Android version to compile against)
   - **minSdk**: 21 (Android 5.0 Lollipop - minimum supported version)
   - **targetSdk**: 36 (Android version app is designed for)

3. **Version Information**:
   - **versionCode**: 1 (internal version number for updates)
   - **versionName**: "1.0" (user-facing version string)

4. **Build Types**:
   - **Release**: 
     - `isMinifyEnabled = false` (no code obfuscation)
     - ProGuard rules defined but not active
   - **Debug**: Default debug configuration (not explicitly defined)

5. **Java Compatibility**:
   - **sourceCompatibility**: Java 11
   - **targetCompatibility**: Java 11
   - Ensures Java 11 language features can be used

6. **Build Features**:
   - **viewBinding**: `true` - Enables View Binding (not currently used in code)

#### Dependencies

**Version Catalog** (`gradle/libs.versions.toml`):
- Centralized dependency version management
- Libraries referenced via aliases (e.g., `libs.appcompat`)

**Core Dependencies**:
- AppCompat, Material, Activity, ConstraintLayout, RecyclerView

**Room Dependencies**:
- `room-runtime`: Runtime library for Room
- `room-compiler`: Annotation processor (generates database code at compile time)

**Lifecycle Dependencies**:
- ViewModel, LiveData, Runtime components

**Security Dependencies**:
- `security-crypto`: EncryptedSharedPreferences

### Compilation Process

1. **Gradle Sync**:
   - Downloads dependencies from Maven repositories
   - Resolves version conflicts
   - Prepares build environment

2. **Annotation Processing**:
   - Room compiler processes `@Entity`, `@Dao`, `@Database` annotations
   - Generates implementation classes:
     - `MemoDatabase_Impl`: Database implementation
     - `MemoDao_Impl`: DAO implementation
     - `Memo_Adapter`: Entity adapter for serialization

3. **Java Compilation**:
   - Compiles all `.java` files to `.class` files
   - Includes generated Room code
   - Java 11 bytecode generated

4. **Resource Processing**:
   - Compiles XML layouts, menus, strings, colors
   - Generates `R.java` file with resource IDs
   - Processes drawable and mipmap resources

5. **DEX Conversion**:
   - Converts Java bytecode to DEX (Dalvik Executable) format
   - Optimizes for Android runtime

6. **Packaging**:
   - Combines code, resources, and manifest
   - Creates APK (Android Package) file

7. **Signing** (Release builds):
   - Signs APK with debug or release key
   - Required for installation on devices

### APK Generation Process

#### Debug APK
- Automatically signed with debug keystore
- Can be installed on any device (development only)
- Located in: `app/build/outputs/apk/debug/app-debug.apk`

#### Release APK
- Must be signed with release keystore (not configured in this project)
- Requires keystore file and credentials
- Located in: `app/build/outputs/apk/release/app-release.apk`

### Build Commands

**Via Gradle Wrapper**:
```bash
# Windows
gradlew.bat assembleDebug
gradlew.bat assembleRelease

# Linux/Mac
./gradlew assembleDebug
./gradlew assembleRelease
```

**Via Android Studio**:
- Build → Make Project (Ctrl+F9)
- Build → Build Bundle(s) / APK(s) → Build APK(s)

### Execution on Device/Emulator

1. **Installation**:
   - ADB install: `adb install app-debug.apk`
   - Or run directly from Android Studio (Shift+F10)

2. **App Launch**:
   - System launcher starts `SplashActivity` (LAUNCHER intent filter)
   - SplashActivity displays for 2 seconds
   - Navigates to MainActivity

3. **Runtime**:
   - Activities created and destroyed as user navigates
   - ViewModel persists across configuration changes
   - Room database initialized on first access
   - LiveData observers update UI reactively

---

## 10. Error Handling & Debugging

### Try-Catch Usage

#### SecurityHelper.java
**Location**: `hashPin()` method
```java
try {
    MessageDigest md = MessageDigest.getInstance("SHA-256");
    // ... hashing logic
} catch (Exception e) {
    return pin; // Fallback
}
```
**Purpose**: Prevents app crash if SHA-256 algorithm is unavailable (unlikely but possible)
**Fallback**: Returns plain PIN (not secure but maintains functionality)

**Location**: `getSharedPreferences()` method
```java
try {
    // EncryptedSharedPreferences creation
} catch (Exception e) {
    return context.getSharedPreferences(PREFS_NAME, Context.MODE_PRIVATE);
}
```
**Purpose**: Handles encryption library failures gracefully
**Fallback**: Uses regular SharedPreferences (still secure, just not encrypted)

#### MemoDetailsActivity.java
**Location**: `onCreate()` method
```java
try {
    memoUid = Integer.parseInt(memoId);
} catch (NumberFormatException e) {
    finish();
    return;
}
```
**Purpose**: Handles invalid memo ID string conversion
**Fallback**: Finishes activity if ID is invalid

### Null Safety Handling

#### MemoAdapter.java
- **Null Checks**: 
  - Checks if `memos` list is null before accessing
  - Validates position before accessing list items
  - Checks if memo fields are null before setting text

#### MainActivity.java
- **View Null Checks**: 
  - Checks if toolbar exists before using: `if (toolbar == null) return;`
  - Checks if buttons exist before setting listeners: `if (btnClearSearch != null)`
- **Empty String Handling**: 
  - Defaults empty search query to empty string
  - Handles null memo title in delete confirmation

#### MemoDetailsActivity.java
- **Null Memo Handling**: 
  - Checks if memo is null after loading
  - Finishes activity if memo not found (may have been deleted)

### Logging (Logcat)

**Current Implementation**: No explicit logging statements in the codebase.

**Potential Improvements**:
- Add Log.d() for debugging database operations
- Add Log.e() for error cases
- Add Log.v() for verbose lifecycle tracking

**Android Studio Logcat**: 
- System automatically logs Activity lifecycle events
- Room database can log SQL queries (if enabled)
- Crash logs appear automatically if app crashes

### Common Runtime Issues Handled

#### 1. Database Threading Issues
**Problem**: Room database operations must not run on main thread
**Solution**: Repository uses ExecutorService for background execution
```java
executor.execute(() -> {
    memoDao.insert(memo);
});
```

#### 2. LiveData Observer Lifecycle
**Problem**: Observers must be removed to prevent memory leaks
**Solution**: 
- ViewModel automatically manages LiveData lifecycle
- Activities observe in `onCreate()` and remove in `onDestroy()` (handled by Lifecycle-aware components)

#### 3. Configuration Changes
**Problem**: Activity recreated on screen rotation, data lost
**Solution**: ViewModel survives configuration changes, data persists automatically

#### 4. Invalid Intent Extras
**Problem**: Memo UID might be missing or invalid
**Solution**: 
- Checks for UID in `onCreate()`
- Validates UID before using
- Finishes activity if invalid

#### 5. Empty Search Results
**Problem**: User searches but no results found
**Solution**: 
- Shows empty search state with helpful message
- Displays search query in message
- Provides clear search button

#### 6. Empty Memo List
**Problem**: No memos exist yet
**Solution**: 
- Shows empty state with icon and message
- Provides "New Memo" button to create first memo

#### 7. PIN Verification Failure
**Problem**: User enters incorrect PIN
**Solution**: 
- Shows toast message "Incorrect PIN"
- Finishes activity to prevent access
- User must restart app and enter correct PIN

#### 8. Concurrent Database Access
**Problem**: Multiple threads accessing database simultaneously
**Solution**: 
- Room handles thread safety internally
- Single database instance (singleton pattern)
- ExecutorService serializes write operations

### Error Prevention Strategies

1. **Input Validation**:
   - PIN length validation (4-6 digits) in PIN settings
   - Null checks before database operations

2. **State Management**:
   - ViewModel manages all UI state
   - Prevents data loss on configuration changes

3. **Type Safety**:
   - Room provides type-safe queries
   - Compile-time verification of database schema

4. **Reactive Updates**:
   - LiveData ensures UI always reflects database state
   - No manual refresh needed (reduces bugs)

---

## 11. Conclusion

### Summary of the Application

**Fast Memo** is a well-architected Android note-taking application that demonstrates modern Android development best practices. The app provides a clean, intuitive interface for creating, organizing, searching, and managing memos with category-based organization and PIN security.

### Key Features Implemented

1. **Complete CRUD Operations**: Create, read, update, and delete memos
2. **Advanced Search**: Real-time search across memo titles and content
3. **Category Filtering**: Filter memos by 7 predefined categories
4. **Multiple Sort Modes**: Sort by date (newest/oldest) or category
5. **PIN Security**: Optional PIN protection for app access
6. **Dark Theme UI**: Modern Material Design 3 interface
7. **Reactive Updates**: LiveData ensures UI always reflects current data
8. **Efficient List Rendering**: DiffUtil optimizes RecyclerView updates

### Strengths of the Implementation

1. **Architecture**: 
   - Clean MVVM architecture with clear separation of concerns
   - Repository pattern abstracts data access
   - ViewModel survives configuration changes

2. **Performance**:
   - Background thread execution for database operations
   - DiffUtil for efficient RecyclerView updates
   - ViewHolder pattern for view recycling

3. **User Experience**:
   - Smooth navigation flow
   - Empty states with helpful messages
   - Confirmation dialogs for destructive actions
   - Relative time formatting for better readability

4. **Security**:
   - PIN hashing with SHA-256
   - Encrypted SharedPreferences for PIN storage
   - Fallback mechanisms prevent crashes

5. **Code Quality**:
   - Well-structured, readable code
   - Consistent naming conventions
   - Proper error handling
   - Modular design

6. **Modern Android Practices**:
   - Room database (recommended over raw SQLite)
   - LiveData for reactive programming
   - Material Design 3 components
   - EdgeToEdge for modern appearance

### Possible Future Improvements

1. **Additional Features**:
   - Voice memos recording and playback
   - Image attachments to memos
   - Memo sharing (export to text, PDF, etc.)
   - Cloud backup/sync (Firebase, Google Drive)
   - Rich text editing (bold, italic, lists)
   - Reminders/notifications for memos
   - Tag system (multiple tags per memo)

2. **UI Enhancements**:
   - Light theme option
   - Custom category colors
   - Swipe gestures (swipe to delete, archive)
   - Grid view option for memo list
   - Memo preview in list items

3. **Performance Optimizations**:
   - Pagination for large memo lists
   - Image compression for attachments
   - Database indexing for faster searches
   - View Binding instead of findViewById

4. **Security Enhancements**:
   - Biometric authentication (fingerprint, face unlock)
   - App lock timeout (auto-lock after inactivity)
   - Encrypted memo content option
   - Secure note deletion (overwrite before delete)

5. **Testing**:
   - Unit tests for ViewModel and Repository
   - Instrumented tests for UI interactions
   - Database migration tests
   - Security testing (PIN brute force protection)

6. **Code Improvements**:
   - Migrate to Kotlin (if preferred)
   - Implement Dependency Injection (Hilt/Dagger)
   - Add comprehensive logging
   - Improve error messages for users

### Final Notes

This application serves as an excellent example of Android development following Google's recommended practices. The MVVM architecture, Room database integration, and Material Design components create a solid foundation for a production-ready note-taking app. The codebase is maintainable, scalable, and demonstrates understanding of Android development best practices.

---

## Appendix: File Reference

### Java Source Files
- `SplashActivity.java` - Launch screen
- `MainActivity.java` - Main memo list screen
- `MemoEditorActivity.java` - Create/edit memo screen
- `MemoDetailsActivity.java` - View memo details screen
- `MemoAdapter.java` - RecyclerView adapter
- `Memo.java` - Data model entity
- `MemoDatabase.java` - Room database
- `MemoDao.java` - Data access object
- `MemoRepository.java` - Repository implementation
- `MemoViewModel.java` - ViewModel for data management
- `SecurityHelper.java` - PIN security utility

### Layout Files
- `activity_main.xml` - Main screen layout
- `activity_memo_editor.xml` - New memo editor layout
- `activity_memo_editor_edit.xml` - Edit memo layout
- `activity_memo_details.xml` - Memo details layout
- `activity_splash.xml` - Splash screen layout
- `item_memo.xml` - RecyclerView item layout
- `empty_search_state.xml` - Empty search state layout

### Configuration Files
- `AndroidManifest.xml` - App manifest
- `build.gradle.kts` - Build configuration
- `libs.versions.toml` - Dependency versions

---

**Document Version**: 1.0  
**Last Updated**: Based on current codebase analysis  
**Author**: Generated Documentation  
**Project**: Fast Memo (NoteMemo) Android Application
