# Nav Resource Managers

A showcase of AI-generated navigation resource management applications. Each app loads from a unified master database of 95+ resources, with local editing capabilities stored in your browser.

## Overview

This project demonstrates how different AI models (GPT, Copilot, Opus, LMC) approach the same application requirements differently. All applications are functionally equivalent Nav Resource Managers, but each reflects the unique design patterns, code style, and UI/UX choices of its generating AI model.

**Recent Updates:**
- **Star/Favorite Resources** - All apps now allow starring resources, which appear at the top of filtered lists
- **Change Tracking** - Export/import changes for merging into master database
- **UI Improvements** - Streamlined toolbar layouts, larger search fields, improved mobile responsiveness

## Quick Start

1. **Start a local web server** (required - see [Why a Server?](#why-a-server) below):
   ```bash
   npx http-server -p 8080
   ```
   Or use VS Code Live Server, Python's `http.server`, or any static file server.

2. **Open in browser**:
   ```
   http://localhost:8080
   ```

3. **Choose an AI model's implementation** from the launch page to explore its approach.

## Applications

| Model | File | UI Style | Notable Characteristics |
|-------|------|----------|------------------------|
| **GPT** | `GPT-NavResourceManager.html` | Clean, modern | Streamlined two-row toolbar, large search field, conventional filters, starred resources, change tracking |
| **Copilot** | `Copilot-NavResourceManager.html` | Card-based | Rich color coding, category badges, inline editing, starred resources, change tracking |
| **Opus** | `Opus-NavResourceManager.html` | Modern, minimal | Clean typography, efficient state management, starred resources, change tracking |
| **LMC** | `LMC-NavResourceManager.html` | Refreshingly simple | Category-organized cards, direct data access, fast filtering, starred resources, change tracking |
| **Mobile** | `Mobile-NavResourceManager.html` | Mobile-first | Touch-optimized, bottom navigation, FAB quick-add, starred resources, change tracking |

## Data Flow

```
┌─────────────────────────────────────────────────────────────┐
│                    master-resources.json                     │
│  (Unified database: 95+ resources, 13 categories)           │
└────────────────────────┬────────────────────────────────────┘
                         │
                         │ ① Fetch on First Launch
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                    Browser Application                       │
└────────────────────────┬────────────────────────────────────┘
                         │
                         │ ② Merge with localStorage (if any edits exist)
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                      Display to User                         │
│  • View all resources                                        │
│  • Search, filter, explore                                  │
│  • Edit any field                                            │
└────────────────────────┬────────────────────────────────────┘
                         │
                         │ ③ Edits Saved to localStorage Only
                         ▼
┌─────────────────────────────────────────────────────────────┐
│                      localStorage                            │
│  (Your edits persist here, not in master file)              │
└─────────────────────────────────────────────────────────────┘
```

### Key Points

- **Master data is read-only** - The `master-resources.json` file is the authoritative source and never modified by the apps
- **Edits are local** - Any changes you make are saved to your browser's localStorage
- **Edits persist** - Your local edits survive browser restarts
- **Edits don't sync** - Changes made in one browser/app don't affect others
- **Always reloadable** - Clear localStorage to reload fresh master data anytime

## Star/Favorite Resources

**All applications** now include a star/favorite feature for quick access to your most-used resources:

### How It Works

- **Star a Resource**: Click the star (☆/⭐) button on any resource card
- **Starred Resources First**: Starred items always appear at the top of filtered lists, regardless of category
- **Persistent**: Your starred resources are saved to localStorage and persist across sessions
- **Visual Indicators**: Starred resources display with highlighted buttons (⭐) and appear first in all views

### Use Cases

- **Quick Access**: Keep frequently-used navigation tools at the top of your list
- **Trip Planning**: Star resources relevant to your current trip planning phase
- **Favorites Management**: Build a personal collection of go-to resources
- **Organization**: Separate must-have tools from the larger database

## Change Tracking & Export

**All applications** now include a change tracking system that enables data collaboration:

### How It Works

1. **Track Changes**: As you add, edit, or delete resources, each app tracks these changes separately
2. **Export Changes**: Export only your changes (not the full dataset) as a JSON file
3. **Merge to Master**: Import the exported changes into `master-resources.json` to update all apps

### Export Format

```json
{
  "version": "1.0.0",
  "exportDate": "2026-05-25T10:30:00Z",
  "appName": "Mobile Nav Resource Manager",
  "changes": {
    "added": [
      {"id": "mob_123", "name": "New Resource", "category": "...", ...}
    ],
    "edited": [
      {"id": "mob_124", "originalId": "abc123", "name": "Updated Name", ...}
    ],
    "deleted": ["def456", "ghi789"]
  }
}
```

### Use Cases

- **Data Curation**: Make edits on mobile, export changes, and merge into master for all users
- **Collaboration**: Multiple users can export their changes for centralized merging
- **Backup**: Export your changes regularly to preserve your contributions
- **Cross-Device Sync**: Export from one device, import on another

### Importing Changes to Master

To merge exported changes into `master-resources.json`:

1. Open the exported JSON file
2. For `added` resources: Append to the `resources` array
3. For `edited` resources: Update existing resources matching `originalId`
4. For `deleted` resources: Remove resources with matching IDs
5. Verify the schema and test with all apps

## Resource Categories

All 13 categories from the master database:

| Category | Resources | Examples |
|----------|-----------|----------|
| **General Navigation** | 12 | Nav apps, GPS tools, offline mapping |
| **Campground Research** | 8 | Campendium, Campspot, Recreation.gov |
| **Route Planning** | 7 | RV Trip Wizard, Mountain Directory |
| **Fuel & Propane** | 6 | GasBuddy, Propane Finder |
| **Dump Stations** | 5 | Sanidumps, RVDumps |
| **RV Parks & Resorts** | 8 | Thousand Trails, KOA, Passport America |
| **Boondocking** | 6 | iOverlander, Campendium, BLM land |
| **Rest Areas & Parking** | 7 | Rest stops, Walmart parking, truck stops |
| **Weather & Road Conditions** | 10 | Weather.gov, Waze, 511 road info |
| **RV Maintenance** | 8 | Repair manuals, mobile techs, parts |
| **Emergency Services** | 6 | RV road service, Poison Control, 911 |
| **Community & Social** | 7 | RV forums, Facebook groups, clubs |
| **Shopping & Services** | 5 | Camping World, RV supply stores |

## Technical Architecture

### Tech Stack

- **Pure HTML/CSS/JavaScript** - Zero dependencies, no build step
- **Vanilla JavaScript** - No frameworks (React, Vue, etc.)
- **localStorage API** - Client-side data persistence
- **Fetch API** - For loading master-resources.json
- **CSS Custom Properties** - For theming and consistency

### Why No Frameworks?

This project showcases AI code generation for:
- **Portable apps** - Run anywhere, no npm install needed
- **Educational code** - Easy to read and understand
- **Comparison** - See how each AI model approaches vanilla JS vs. framework defaults

### File Structure

```
nav-resources/
├── index.html                          # Launch page with app cards and "Open All Apps"
├── master-resources.json               # Unified database (95+ resources)
├── GPT-NavResourceManager.html         # GPT-generated app (streamlined UI)
├── Copilot-NavResourceManager.html     # Copilot-generated app
├── Opus-NavResourceManager.html        # Opus-generated app
├── LMC-NavResourceManager.html         # LMC-generated app
├── Mobile-NavResourceManager.html      # Mobile-optimized with change tracking
└── README.md                           # This file
```

### Index Page Features

The launch page (`index.html`) provides:
- **App Cards**: Visual overview of all 5 resource managers with descriptions and tags
- **Open All Apps**: Launch all apps simultaneously (with popup blocker handling)
- **Centered Layout**: Applications section aligned with grid boundaries for clean appearance
- **Quick Access**: Click "Open App" on any card to launch that specific manager

## Why a Server?

You **cannot** open these files directly from your filesystem (e.g., `file:///C:/Users/.../index.html`) because browsers block fetch() requests to local files for security (CORS policy).

**Solution: Use any local web server:**

| Option | Command | Notes |
|--------|---------|-------|
| **npx http-server** | `npx http-server -p 8080` | Simplest, no install |
| **VS Code Live Server** | Right-click → "Open with Live Server" | Great for development |
| **Python** | `python -m http.server 8080` | Built into Python |
| **PHP** | `php -S localhost:8080` | Built into PHP |
| **Node.js** | `npx serve` | Alternative to http-server |

Then open `http://localhost:8080` in your browser.

## Data Persistence

### Master Data (master-resources.json)

- **Location**: `master-resources.json` in project root
- **Purpose**: Authoritative source for all 95+ resources
- **Schema Version**: 2.0.0
- **Access**: All apps fetch this on first launch
- **Read-only**: Apps never modify this file

### Local Data (localStorage)

- **Location**: Your browser's localStorage (per app, per domain)
- **Purpose**: Store your edits, additions, deletions
- **Key Format**: `{model}_nav_data` (e.g., `gpt_nav_data`)
- **Scope**: Specific to each app/browser
- **Survives**: Browser restarts
- **Cleared by**: Clear browser data or explicit reset

### Data Loading Sequence

1. App starts → Attempt fetch from `master-resources.json`
2. If fetch succeeds → Load master data
3. Check localStorage for existing edits → Merge if present
4. If fetch fails (no server) → Load from localStorage or use embedded defaults
5. Display unified data to user

## Feature Comparison Across AI Models

All five apps share core functionality:
- ✅ View all 95+ resources
- ✅ Search by name/description
- ✅ Filter by category
- ✅ Filter by offline availability
- ✅ Edit resource details
- ✅ Add new resources
- ✅ Delete resources
- ✅ Star/favorite resources
- ✅ Persistent storage (localStorage)
- ✅ Change tracking (added/edited/deleted)
- ✅ Export changes (JSON)
- ✅ Import changes (merge)
- ✅ Clear tracked changes
- ✅ Responsive design

**Differences are in:**
- UI/UX design patterns
- Code organization and style
- State management approaches
- Visual design and theming
- Interaction patterns

## Common Issues

### "master jason does not exist" error

**Cause**: Browser blocked fetch() due to CORS/file:// protocol restrictions

**Fix**: Start a local web server (see [Why a Server?](#why-a-server) above)

### App shows fewer than 95 resources

**Cause**: 
- Browser cached old version
- localStorage has stale data
- Master data fetch failed silently

**Fix**:
1. Hard refresh browser (Ctrl+Shift+R / Cmd+Shift+R)
2. Open browser DevTools Console and check for errors
3. Clear localStorage for that app:
   ```javascript
   // In DevTools Console:
   localStorage.clear(); // Or specific key like: localStorage.removeItem('gpt_nav_data');
   ```
4. Ensure web server is running

### Edits not appearing

**Cause**: Edits are saved to localStorage, not master file

**Expected behavior**: Edits persist in your browser only. To share changes, use the Export Changes feature and merge into `master-resources.json`

### GPT Manager Issues

**Historical Issue**: "document is not a function" error

**Cause**: JavaScript scope and DOM loading problems where functions were defined inside DOMContentLoaded but referenced from outer scope.

**Fix Applied**: Complete JavaScript restructure:
- All state variables declared in outer scope before DOMContentLoaded
- All functions defined outside DOMContentLoaded for proper access
- DOM element references populated inside DOMContentLoaded listener
- Consistent use of `document.getElementById()` (not `document()`)

**Current Status**: All issues resolved. The GPT Manager now features a streamlined two-row toolbar layout with large search field, conventional filters, and full change tracking support.

If you encounter any loading issues, ensure the app is being served by a web server (not opened directly via file://) and refresh the page.

## Development

### Adding Resources to Master Database

Edit `master-resources.json`:

```json
{
  "resources": [
    {
      "id": "unique-id",
      "name": "Resource Name",
      "category": "Category Name",
      "url": "https://example.com",
      "description": "Brief description",
      "offlineCapable": false,
      "tags": ["tag1", "tag2"]
    }
  ]
}
```

Then reload any app to fetch the updated master data.

### Modifying an App

Each HTML file is self-contained:
1. Open in any text editor
2. Edit HTML, CSS, or JavaScript
3. Save and refresh browser
4. No build step required

## Browser Compatibility

- **Best**: Modern browsers (Chrome, Edge, Firefox, Safari)
- **Required**: ES6+ support (arrow functions, async/await, fetch, localStorage)
- **Tested**: Chrome 120+, Edge 120+, Firefox 120+, Safari 17+

## License

This project is provided as-is for educational and comparative purposes.

## Credits

**Purpose**: This project showcases AI-generated code and should not be used as an example of human best practices. Each app reflects how different AI models (GPT, Copilot, Opus, LMC) interpret and implement the same requirements.

**Master Data**: Curated from the RV navigation community and represents real-world resources used by RV enthusiasts.
