# Minimum Movie Recommendation System

This project implements a very basic content-based movie recommendation system using Python. It uses mock data for movies and user preferences (liked movies) and recommends movies based on shared genres.

## Project Structure

- `.glyph/`: Contains task management files for the Glyph Protocol.
  - `tasks/`: Task definition files.
  - `plans/`: Detailed execution plans for tasks.
  - `logs/`: Observational logs.
- `src/`:
  - `mock_data.py`: Contains the mock movie data (list of movies with IDs, titles, and genres) and mock user ratings (dictionary of user IDs to lists of liked movie IDs).
  - `recommender.py`: Contains the core recommendation logic. It includes functions to:
    - Get genres preferred by a user based on their liked movies.
    - Recommend new movies that match these preferred genres and haven't been liked/seen by the user.
  - `main.py`: Provides a simple command-line interface (CLI) to interact with the system. Users can input their user ID to get movie recommendations.
- `README.md`: This file.

## How to Run

1.  Ensure you have Python 3 installed.
2.  Navigate to the project's root directory in your terminal.
3.  Run the command-line interface using:
    ```bash
    python src/main.py
    ```
4.  The CLI will prompt you to enter a user ID (e.g., `user1`, `user2` - see `src/mock_data.py` for available mock users).
5.  The system will then print a list of recommended movies for that user.

## System Logic

The recommendation logic is content-based and works as follows:

1.  **Identify Liked Genres:** For a given user, the system looks at the movies they have liked (as defined in `user_ratings` in `mock_data.py`). It extracts all unique genres from these liked movies.
2.  **Find Candidate Movies:** It then searches through the entire movie list (`movies` in `mock_data.py`) for movies that the user has *not* yet liked.
3.  **Match Genres:** For each unliked movie, it checks if its genres overlap with the user's liked genres.
4.  **Score and Rank:** Movies are scored based on the number of matching genres. The more genres a movie shares with the user's preferred genres, the higher its score.
5.  **Recommend:** The system recommends the top N movies with the highest match scores.

## Limitations

-   **Mock Data:** Uses a very small, predefined set of mock data.
-   **Simple Algorithm:** The genre-matching algorithm is basic. It doesn't consider nuanced preferences, movie popularity, user similarity (collaborative filtering), or other advanced recommendation techniques.
-   **No Learning:** The system does not learn or adapt based on new ratings or interactions beyond the initial mock data.
-   **Basic CLI:** The user interface is a very simple command-line tool.

This project serves as a minimal example of a recommendation system concept.

# 🔮 Glyph Tasks Dashboard

A standalone HTML visualization tool for Glyph Protocol task and plan files. No dependencies required - just open in your browser!

**✅ Now Available:** The dashboard has been implemented as `glyph_dashboard.html` in the root directory.

## Features

- 📊 **Interactive Visualizations**
  - **Overview**: Task cards with quick overview and click-for-details
  - **Plans**: Execution plans with subtask progress tracking and visual breakdowns
  - **Timeline**: Chronological view with optional subtask display and zoom/pan
  - **Status Flow**: Kanban-style board with tasks grouped by workflow status

- 📈 **Comprehensive Statistics**: Task counts, plan metrics, subtask progress, and completion tracking

- 🎯 **Detailed Task Views**: Click on any task to see comprehensive details including:
  - Subtask execution logs with timestamps
  - Final output summaries and artifacts
  - Error details and clarification requests
  - Full task history and status changes

- 🎮 **Interactive Controls**:
  - **Pan & Zoom**: Mouse wheel zoom and drag to navigate large graphs
  - **Reset Zoom**: Return to original view
  - **Fit to View**: Auto-resize graphs to fit content

- 📁 **Simple Loading Options**:
  - **Auto-load**: Automatically detects `.glyph` directory when served from web server
  - **Drag & drop**: Simply drag your `.glyph` folder to the browser

## Quick Start

### Option 1: Auto-loading (Recommended)
1. Place `glyph_dashboard.html` in the same directory as your `.glyph` folder:
   ```
   your-project/
   ├── .glyph/
   │   ├── tasks/
   │   └── plans/
   └── glyph_dashboard.html
   ```

2. Start a simple web server in that directory:
   ```bash
   # Python 3
   python -m http.server 8000
   
   # Python 2  
   python -m SimpleHTTPServer 8000
   
   # Node.js (if you have npx)
   npx serve .
   ```

3. Open `http://localhost:8000/glyph_dashboard.html`
4. The dashboard will **automatically** detect and load your `.glyph` files!

### Option 2: Drag & Drop (Any Browser)
1. Download `glyph_dashboard.html`
2. Open it directly in your browser
3. Drag and drop your `.glyph` folder onto the interface
4. All task and plan files will be loaded instantly

### Option 3: File-based Usage (Limited)
1. Download `glyph_dashboard.html`
2. Open it directly by double-clicking (opens in browser)
3. You'll see helpful guidance for setting up auto-loading
4. Use drag & drop as the primary method for this approach

## Visualizations

### Overview
- Task cards showing ID, title, status, priority, and effort
- Click any card to see comprehensive task details
- Visual status indicators and dependency counts

### Plans View
- **Execution Plans**: Cards showing plan progress and subtask breakdowns
- **Progress Bars**: Visual completion percentage with color coding
- **Status Distribution**: Count of completed (✅), in-progress (⏳), and blocked (🚫) subtasks
- **Plan Metadata**: Generation dates and parent task relationships
- **Interactive**: Click plan cards to view parent task details

### Timeline View
- Shows tasks arranged chronologically by submission date
- **Subtask Toggle**: Optional "Show Subtasks" checkbox for detailed execution view
- **Visual Hierarchy**: Tasks as full circles, subtasks as smaller circles with reduced opacity
- Circle size and color indicate status
- **Interactive Elements**: Click tasks or subtasks to view details
- Useful for tracking project progress over time

### Status Flow View
- Groups tasks into columns by status
- Great for kanban-style workflow visualization
- Shows bottlenecks and work distribution

## File Format Support

The dashboard parses standard Glyph Protocol files:

- **Task files**: `.glyph/tasks/GLYPH#TASK_*.md`
- **Plan files**: `.glyph/plans/GLYPH#TASK_*_plan.md`

## Browser Compatibility

- ✅ Chrome/Edge/Safari (modern versions)
- ✅ Firefox (modern versions)
- ✅ Mobile browsers
- ⚠️  IE11+ (limited support)

## Tips

- **Interactive**: Click on any node in the graphs to see task details
- **Responsive**: Works on desktop, tablet, and mobile
- **No data sent**: Everything runs locally in your browser
- **Fast**: Handles dozens of tasks smoothly
- **Offline**: Works without internet connection

## Troubleshooting

**Q: Auto-loading doesn't work**
A: Make sure you're serving the HTML file via HTTP (not opening directly), and that the `.glyph` folder is in the same directory.

**Q: Some tasks don't show relationships**
A: Check that your task files have properly formatted `Dependencies` arrays and that plan files exist for complex tasks.

**Q: Graph looks cramped**
A: Try switching between different graph views or using the browser's zoom functionality.

## Example Structure

Your project should look like this for auto-loading:
```
my-project/
├── .glyph/
│   ├── tasks/
│   │   ├── GLYPH#TASK_20240101120000_ABC123.md
│   │   └── GLYPH#TASK_20240101130000_DEF456.md
│   └── plans/
│       ├── GLYPH#TASK_20240101120000_ABC123_plan.md
│       └── GLYPH#TASK_20240101130000_DEF456_plan.md
├── glyph_dashboard.html
└── README.md
```

## Recent Improvements

### v2.3 - Comprehensive Plan & Subtask Visualization (December 2024)
- 📊 **New Plans tab**: Dedicated visualization for execution plans with progress tracking
- 📈 **Enhanced statistics**: Added plan counts and subtask completion metrics
- 🎯 **Plan cards**: Progress bars, status distribution, and subtask breakdowns
- 📅 **Timeline with subtasks**: Optional toggle to show subtasks in chronological view
- 🎨 **Visual hierarchy**: Clear differentiation between tasks, plans, and subtasks

### v2.2 - Enhanced UX and Zoom Fixes (December 2024)
- 🔍 **Fixed graph zoom**: Zoom now affects only graph content, not entire page
- 🗂️ **Streamlined interface**: Removed dependencies tab (no task dependencies exist)
- 📋 **Enhanced task modals**: Comprehensive task details with proper markdown formatting
- 🎨 **Improved visual design**: Better typography, color coding, and structured layouts
- 🎯 **Better debugging**: Added console logging for troubleshooting modal issues

### v2.1 - Critical Bug Fixes (December 2024)
- ✅ **Fixed tab switching**: All visualization tabs now display content properly
- ✅ **Resolved console errors**: Eliminated browser warnings and negative radius errors
- ✅ **Enhanced interactivity**: Overview task cards are now clickable with modal details
- ✅ **Improved UX**: Better hover effects and visual feedback for clickable elements
- ✅ **Performance optimizations**: Fixed event listener warnings and graph rendering

### v2.0 - Full Visualization Suite (December 2024)
- 🎨 **Complete graph implementations**: Dependencies, Timeline, and Status Flow visualizations
- 🔍 **Enhanced subtask rendering**: Comprehensive execution logs and output summaries
- 🎮 **Interactive features**: Pan, zoom, and navigation controls for all graphs
- 📱 **Responsive design**: Improved mobile and tablet compatibility
- 🚀 **Universal compatibility**: Works with any Glyph Protocol project structure

---

**Made for the Glyph Protocol** - Simple, powerful, dependency-free task visualization! 🚀 