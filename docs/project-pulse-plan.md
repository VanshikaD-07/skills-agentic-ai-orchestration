# Project Pulse Dashboard Implementation Plan

## Summary

Mona's Project Pulse dashboard is a lightweight static web application that displays project status, ownership, and activity for contributors. The dashboard consists of three core files (`app/index.html`, `app/styles.css`, `app/project-data.json`) and a VS Code launch configuration (`.vscode/launch.json`). The work divides naturally into parallel design and infrastructure tracks, followed by sequential integration and validation. The Designer creates visual language and styling hooks; the Coder implements the data model, HTML structure, and launch configuration. Both specialists can work in parallel on their assigned scopes, then coordinate for final assembly.

## Ordered Implementation Steps

### Phase 1: Data Model & Structure Definition (Sequential, Prerequisite)
**Owner:** Coder  
**Files:** `app/project-data.json`  
**Dependencies:** None  
**Parallel blocker:** No (this is the prerequisite for all downstream work)

**Tasks:**
1. Define the `app/project-data.json` schema with a `projects` array
2. Create sample project objects with required fields: `name`, `owner`, `status`, `recentActivity`, `priority`
3. Include 4–6 realistic sample projects with varied status and priority levels
4. Ensure JSON is valid and parseable

**Validation:**
- File exists and contains valid JSON
- All required fields present in each project object
- Data is realistic and representative of actual project states

### Phase 2: Parallel Track A – Designer UI/UX & Styling
**Owner:** Designer  
**Files:** `app/styles.css`  
**Dependencies:** Waits for Phase 1 data model (to understand content scale)  
**Can run in parallel with:** Phase 2 Track B (after Phase 1 complete) and Phase 3 (independent scope)

**Tasks:**
1. Define design system:
   - Color palette (background, primary, status indicators, text)
   - Typography scale and font families
   - Spacing/padding rules (8px grid assumed)
   - Responsive breakpoints (mobile, tablet, desktop)
2. Design dashboard layout:
   - `.dashboard` container with max-width and centering
   - Project card grid (responsive 1–3 columns)
   - Information hierarchy for card content
3. Create CSS components with deterministic hooks:
   - `.project-card` — outer container with shadow, rounded corners, hover state
   - `.project-header` — name and owner section
   - `.project-status` — badge styling for active/paused/completed/at-risk
   - `.project-activity` — recent activity display
   - `.project-priority` — visual treatment for priority levels
   - `.project-summary` — contributor-friendly description text
4. Accessibility & readability:
   - WCAG AA contrast ratios
   - Clear visual affordances (shadows, borders)
   - Readable spacing, line-height, and font sizes
   - Semantic color use (e.g., red for at-risk, green for active)
5. Responsive behavior:
   - Mobile-first or graceful desktop enhancement
   - Card stack on small screens, grid layout on larger
   - Touch-friendly interactive areas

**Validation:**
- CSS file exists and is syntactically valid
- All design hooks (`.dashboard`, `.project-card`, etc.) are defined
- Colors meet WCAG AA contrast minimums
- Layout responsive across common viewport sizes
- No hardcoded content (classes only, no element-specific styles that assume HTML structure)

### Phase 2: Parallel Track B – Coder HTML Structure
**Owner:** Coder  
**Files:** `app/index.html`  
**Dependencies:** Waits for Phase 1 data model schema  
**Can run in parallel with:** Phase 2 Track A (after Phase 1 complete)

**Tasks:**
1. Create HTML skeleton:
   - DOCTYPE, meta viewport, meta charset
   - Title and page description
   - Link to `styles.css`
   - Script tag to load `project-data.json`
2. Implement dashboard container structure:
   - `.dashboard` wrapper
   - Header section with dashboard title
3. Create project card template/loop:
   - Iterate through `projects` array from JSON
   - Render each project with:
     - `.project-card` container
     - `.project-header` with name and owner
     - `.project-status` badge
     - `.project-activity` display
     - `.project-priority` indicator
     - `.project-summary` paragraph
4. Implement data loading logic:
   - Fetch `project-data.json`
   - Parse and validate required fields
   - Handle missing data gracefully (default values or skip)
   - Clear error reporting if JSON is malformed
5. Ensure semantic HTML:
   - Use `<article>` or `<section>` for project cards
   - Heading hierarchy (h1 for dashboard, h2/h3 for projects)
   - List elements where appropriate (e.g., activity items)
   - Proper alt text concepts (no images in MVP)

**Validation:**
- HTML is valid (can be checked with W3C validator or linter)
- Class names match Designer's CSS hooks exactly
- `project-data.json` is loaded and rendered
- No console errors when opening in browser
- All required fields displayed (even if empty)

### Phase 3: Launch Configuration (Sequential, Independent)
**Owner:** Coder  
**Files:** `.vscode/launch.json`  
**Dependencies:** None (can run in parallel with Phase 2 tracks, but sequenced here for clarity)  
**Blocks:** Nothing (pure infrastructure)

**Tasks:**
1. Create `.vscode/launch.json` with strict JSON (no comments)
2. Configure launch task:
   - Name: `"Run Project Pulse Dashboard"`
   - Type: `"chrome"` or `"firefox"` (learner's preference)
   - URL: `"http://localhost:5000/index.html"` (or appropriate port)
   - Working directory: `"${workspaceFolder}/app"`
   - Server command: Use Python simple HTTP server, Node http-server, or VS Code Live Server
   - Ensure `index.html` opens directly (not directory listing)
3. Ensure configuration:
   - Uses deterministic port number
   - Follows VS Code launch.json conventions
   - Is discoverable in the "Run and Debug" menu

**Validation:**
- Launch configuration is valid JSON (can parse without errors)
- Configuration opens `index.html` directly (learner can test by clicking "Run Project Pulse Dashboard")
- No errors in VS Code Debug console

### Phase 4: Integration & Cross-File Validation (Sequential, Final)
**Owner:** Coder (primary), Designer (review)  
**Files:** All (read-only review)  
**Dependencies:** Phase 1, Phase 2A, Phase 2B, Phase 3 must be complete  
**Blocks:** Delivery

**Tasks:**
1. Coder verifies:
   - `app/index.html` loads without errors
   - `app/project-data.json` is fetched and rendered correctly
   - All CSS classes from HTML match Designer's CSS hooks
   - Launch configuration starts the server and opens the dashboard
   - Browser console shows no errors or warnings
2. Designer reviews:
   - Visual appearance matches design intent
   - Spacing, typography, and colors are consistent
   - Status badges and priority indicators are visually distinct
   - Responsive behavior works on multiple viewport sizes
   - Accessibility features (contrast, focus states) are functional
3. Joint validation:
   - Dashboard displays project information clearly
   - All required fields visible: name, owner, status, recentActivity, priority
   - Cards are readable and well-spaced
   - No broken image references or missing assets
   - User can easily distinguish active, paused, completed, and at-risk projects

**Validation:**
- No console errors or warnings
- All sample projects render correctly
- Visual design is polished and dashboard-like (not a bare list)
- Responsive layout works on mobile, tablet, and desktop viewports
- Launch config successfully opens the dashboard in browser

## File Assignments Summary

| File | Owner | Responsibilities |
|------|-------|------------------|
| `app/project-data.json` | Coder | Schema definition, sample data, JSON validity |
| `app/index.html` | Coder | HTML structure, semantic markup, data loading logic, CSS hook integration |
| `app/styles.css` | Designer | Visual design, layout, typography, color system, responsive behavior, accessibility |
| `.vscode/launch.json` | Coder | Launch configuration, server setup, deterministic naming and ports |

## Dependencies Between Steps

- Phase 1: Data Model (Coder) → prerequisite
- Phase 2A: Styling (Designer) and Phase 2B: HTML (Coder) can run in parallel after Phase 1
- Phase 3: Launch Config (Coder) can run independently, but is easiest to finalize after Phase 2B
- Phase 4: Integration & Validation requires Phases 1, 2A, 2B, and 3 to be complete

**Critical path:** Phase 1 → Phase 2A + Phase 2B (parallel) → Phase 3 → Phase 4

## Work That Can Run in Parallel

- After Phase 1 completes, Designer can build `app/styles.css` while Coder builds `app/index.html`
- Coder can prepare `.vscode/launch.json` independently once the app structure is known
- Integration waits until all assigned files are ready

## Work That Must Run Sequentially

- Phase 1 must finish before Phase 2A and Phase 2B start
- Phase 4 must wait for Phases 1, 2A, 2B, and 3
- Launch configuration should be checked after the HTML entry point exists

## Edge Cases to Handle

1. Missing project fields
2. Large project names or descriptions
3. Unknown status values
4. Empty projects array
5. CORS or fetch failures
6. Browser compatibility
7. Launch config port conflict
8. Status badge styling ambiguity
9. Card layout on very small screens
10. Responsive images or icons

## Validation Expectations

### After Phase 1
- `app/project-data.json` exists and contains valid JSON
- All required fields are present
- Sample data is realistic and varied

### After Phase 2A
- `app/styles.css` exists and is syntactically valid CSS
- All required design hooks are defined
- Colors meet WCAG AA contrast minimums
- Responsive layout works across common viewports
- Hover/focus states are visible

### After Phase 2B
- `app/index.html` is valid HTML
- Page loads without console errors
- `project-data.json` is fetched and rendered
- All CSS class names match the stylesheet
- Semantic HTML is used

### After Phase 3
- `.vscode/launch.json` is valid JSON
- The launch config appears in VS Code Run and Debug
- The dashboard opens directly, not a directory listing
- The configured server starts cleanly

### After Phase 4
- Dashboard loads and displays all sample projects
- Visual design is polished and dashboard-like
- Responsive layout works across viewports
- No browser console errors or warnings
- Status badges are accessible and distinct
- No broken image references or missing assets
- Launch configuration opens the dashboard without manual server start

## Open Questions

1. HTTP Server choice for launch config
2. Default port number
3. Status and priority values
4. Project card content order
5. Accessibility requirements scope
6. Project activity display format
7. Styling framework or approach
8. Mobile-first or desktop-first design
9. Sample data volume
10. Localization/internationalization

## Implementation Timeline & Effort Estimate

| Phase | Owner | Estimated Effort | Critical Path |
|-------|-------|------------------|---|
| Phase 1: Data Model | Coder | 15–20 min | Yes (prerequisite) |
| Phase 2A: Styling | Designer | 30–45 min | Parallel |
| Phase 2B: HTML | Coder | 30–40 min | Parallel |
| Phase 3: Launch Config | Coder | 10–15 min | After Phase 2B |
| Phase 4: Integration & Validation | Coder + Designer | 20–30 min | Final gate |
| **Total** | | **105–150 min** | |

## Success Criteria

The Project Pulse dashboard implementation is complete when:

1. All four required files exist and are properly structured
2. Data model is defined with sample projects covering all status and priority types
3. HTML renders all projects from JSON without console errors
4. CSS provides a polished, dashboard-like visual experience with clear information hierarchy
5. Responsive layout works on mobile, tablet, and desktop viewports
6. Launch configuration successfully opens the dashboard with a single VS Code click
7. Accessibility standards are met
8. No broken image references, missing files, or unhandled errors
9. Both Designer and Coder have completed their assigned scopes without file conflicts
10. Documentation and comments are clear enough for a learner to understand the orchestration

*Plan created: 2026-06-10*  
*Prepared for Orchestrator delegation via GitHub Copilot CLI*
