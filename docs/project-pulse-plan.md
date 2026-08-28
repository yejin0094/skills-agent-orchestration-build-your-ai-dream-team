# Project Pulse Dashboard Implementation Plan

## Summary

Build Mona's Project Pulse as a polished, responsive static dashboard that helps contributors quickly understand project health. The dashboard will present projects as visually distinct cards containing the project name, owner, current status, recent activity, priority or risk level, and a short contributor-friendly summary.

The application will use:

- Semantic HTML in `app/index.html`
- A top-level `projects` data array in `app/project-data.json`
- Responsive, accessible visual styling in `app/styles.css`
- A VS Code launch configuration in `.vscode/launch.json`

The launch configuration must serve the `app/` directory and open `index.html` directly so learners see the dashboard rather than a directory listing.

## Agent Responsibilities

### Designer

The Designer owns the visual and experience direction for the dashboard, including:

- Information hierarchy for the dashboard header, project overview, and cards
- Page layout, spacing, typography, color palette, and visual rhythm
- Project-card composition and responsive grid behavior
- Status-badge and priority-treatment design
- Accessibility considerations, including contrast, focus states, semantic styling, and readable content
- Responsive behavior for desktop, tablet, and mobile widths
- Visual polish such as borders, rounded corners, shadows, hover states, and empty-state presentation

The Designer owns `app/styles.css` and should provide implementation guidance to the Coder for the HTML hooks and class names required by the stylesheet.

### Coder

The Coder owns the structural and data-oriented implementation, including:

- Semantic dashboard markup and project-card structure
- Loading and rendering project data from JSON
- Consistent status, priority, owner, and activity fields
- Browser-friendly error handling if project data cannot be loaded
- VS Code launch configuration for running the static app
- Validation that all files are correctly linked and runnable

The Coder owns:

- `app/index.html`
- `app/project-data.json`
- `.vscode/launch.json`

The Coder must not modify `app/styles.css` unless the Orchestrator explicitly reassigns a narrowly scoped integration fix.

## Ordered Implementation Steps

### 1. Confirm requirements and establish the contract

**Owner:** Orchestrator, with Planner input  
**Files:** No implementation files

Review `.github/project-pulse-brief.md` and establish the shared contract:

- The app is a static dashboard rooted at `app/`
- The page must visibly identify itself as Project Pulse
- Project cards must show status, recent activity, priority, owner, and summary information
- Data must be stored in a top-level `projects` array
- CSS must expose predictable hooks such as `.dashboard` and `.project-card`
- The launch configuration must use `${workspaceFolder}/app` as its working directory and open `index.html`

The Orchestrator should communicate this contract to both specialists before implementation begins.

### 2. Define the visual system and responsive behavior

**Owner:** Designer  
**File assignment:** `app/styles.css`

Create the styling direction and implement the stylesheet. The design should include:

- A clear dashboard shell with a professional header
- A responsive project-card grid
- Readable metadata groupings
- Distinct status badges with text labels, not color alone
- Clear priority or risk indicators
- Rounded card surfaces, subtle shadows, borders, and consistent spacing
- Typography with strong heading hierarchy and comfortable body text
- Hover and keyboard-focus states that do not reduce readability
- Breakpoints that collapse the grid cleanly on smaller screens
- Mobile-safe spacing and text wrapping
- Sufficient color contrast for text, badges, and controls

The Designer should document or communicate the expected HTML class hooks before the Coder finalizes the markup.

### 3. Create representative project data

**Owner:** Coder  
**File assignment:** `app/project-data.json`

Create valid JSON with a top-level `projects` array. Include several representative projects so the layout can be evaluated realistically. Every project should include:

- `name`
- `owner`
- `status`
- `recentActivity`
- `priority`
- A short contributor-friendly summary, using the agreed field name and markup contract

The sample set should include varied statuses and priorities, such as active, at-risk, blocked, or complete, so badge and priority styling can be validated. Values should be deterministic, concise, and realistic.

### 4. Implement the dashboard structure

**Owner:** Coder  
**File assignment:** `app/index.html`

Build the page structure using semantic HTML. Include:

- Document metadata and an accessible page title
- A Project Pulse heading and short explanatory subtitle
- A main dashboard container with the `.dashboard` hook
- A project-card region that can contain multiple `.project-card` elements
- Card content for project name, owner, status, recent activity, priority, and summary
- Status and priority elements with meaningful text and accessible labeling
- A data-loading/rendering mechanism connected to `project-data.json`
- A clear error state if the JSON cannot be loaded or is malformed
- A stylesheet reference to `styles.css`

Keep the markup compatible with the Designer's stylesheet and avoid embedding large amounts of presentation styling directly in HTML.

### 5. Configure the VS Code launch experience

**Owner:** Coder  
**File assignment:** `.vscode/launch.json`

Create strict JSON containing a deterministic configuration named **Run Project Pulse Dashboard**. The configuration must:

- Serve files from `${workspaceFolder}/app`
- Set the working directory to `${workspaceFolder}/app`
- Open `index.html` directly
- Avoid opening a directory listing
- Use an available, predictable local port and the repository's supported preview mechanism
- Remain valid JSON without comments

The Coder should align the configuration with the tools available in the Codespace and existing repository conventions.

### 6. Integrate the structure, data, and design

**Owner:** Orchestrator coordinating Designer and Coder  
**Files:** All assigned files

Review the completed files as one integrated surface. Resolve only cross-file integration issues, such as:

- HTML class names not matching CSS selectors
- Data field names not matching the rendering logic
- Missing stylesheet or JSON references
- Status or priority values that do not have a visual treatment
- Layout overflow caused by unexpectedly long content
- Launch configuration paths that do not resolve from the workspace

Ownership should remain separated: the Designer continues to own styling changes, while the Coder owns HTML, JSON, and launch configuration changes.

### 7. Validate and hand off

**Owner:** Orchestrator, with Designer and Coder validation input  
**Files:** All implementation files

Perform the validation listed below, record any limitations, and confirm that the learner can launch the app using **Run Project Pulse Dashboard**.

## File Assignments

| File | Primary owner | Responsibility |
| --- | --- | --- |
| `app/index.html` | Coder | Semantic dashboard structure, project-card markup, data loading, accessible labels, and error state |
| `app/styles.css` | Designer | UI/UX styling, visual design, responsive layout, badges, priority treatment, and accessibility states |
| `app/project-data.json` | Coder | Valid sample project records and the top-level `projects` array |
| `.vscode/launch.json` | Coder | VS Code launch configuration serving `app/` and opening `index.html` |

The Designer may review the HTML contract and request class-hook changes, but should not edit `app/index.html`. The Coder may request CSS hooks, but should not edit `app/styles.css`. This prevents conflicting edits.

## Dependencies

- Step 1 must happen first because both specialists need the same data and markup contract.
- Designer styling and Coder data creation can begin after Step 1 and can run in parallel.
- Coder HTML implementation depends on the Designer's agreed class hooks, but the Coder can scaffold semantic structure in parallel if the hooks are finalized early.
- The HTML rendering logic depends on the JSON field names being agreed upon.
- Launch configuration depends on the final entry point being `app/index.html`.
- Integration and end-to-end validation must happen after the assigned files exist.
- Final launch verification must happen after all path and rendering dependencies are integrated.

## Parallel Work

The following work can run in parallel after the contract is established:

- **Designer:** implement `app/styles.css`, define the visual system, responsive breakpoints, badge treatments, and required CSS hooks.
- **Coder:** create `app/project-data.json` and `.vscode/launch.json`.
- **Coder:** scaffold the semantic portions of `app/index.html`, provided the agreed class names and data fields are used.

The Designer and Coder must communicate the shared class and data-field contract before integration. Parallel work should not involve both agents editing the same file.

## Sequential Work

These activities must remain sequential:

1. Requirements and ownership agreement before implementation.
2. Agreement on CSS hooks and JSON field names before final HTML rendering is completed.
3. Data and HTML integration before visual integration review.
4. All implementation files completed before launch testing.
5. Launch testing and responsive review before the Orchestrator's final handoff.

## Edge Cases to Handle

- Empty `projects` array: show a clear, intentional empty state rather than a blank dashboard.
- Missing or malformed JSON: show a visible data-loading error and avoid rendering misleading cards.
- Missing optional summary or activity text: preserve card structure and display an appropriate fallback label.
- Unknown status or priority value: retain the text value and use a neutral visual treatment rather than failing.
- Long project names, owner names, summaries, or activity descriptions: wrap or truncate without causing horizontal overflow.
- Many projects: keep the grid usable and avoid fixed heights that clip content.
- Narrow mobile screens: stack cards and metadata without requiring horizontal scrolling.
- Keyboard navigation: ensure interactive elements have visible focus states.
- Color-vision limitations: communicate status and priority with text, labels, or icons in addition to color.
- Reduced-motion preferences: avoid requiring animation and respect `prefers-reduced-motion` if transitions are included.
- Local-file restrictions: ensure the launch configuration serves the app over a local web server so JSON loading works reliably.
- Incorrect launch working directory: verify paths resolve from `${workspaceFolder}/app`, not from the repository root.

## Validation Expectations

### Structural validation

- Confirm `app/index.html`, `app/styles.css`, `app/project-data.json`, and `.vscode/launch.json` exist.
- Confirm `index.html` references both `styles.css` and `project-data.json`.
- Parse `project-data.json` as strict JSON.
- Confirm the JSON contains a top-level `projects` array.
- Confirm project records include `name`, `owner`, `status`, `recentActivity`, and `priority`.
- Confirm `.vscode/launch.json` is strict JSON and contains **Run Project Pulse Dashboard**.
- Confirm the launch configuration uses `app/` as its working directory and opens `index.html`.

### Visual and UX validation

- Launch the app using **Run Project Pulse Dashboard**.
- Confirm the browser opens the Project Pulse dashboard rather than a server directory listing.
- Confirm multiple project cards render from the JSON data.
- Confirm each card visibly presents project name, owner, status, recent activity, priority, and summary.
- Confirm status badges and priority treatments are distinguishable and readable.
- Confirm the design looks polished rather than like bare HTML.
- Review desktop, tablet, and mobile viewport widths.
- Check that long content does not create horizontal scrolling or clipped card content.
- Check text contrast, focus visibility, semantic headings, and non-color status communication.
- Confirm the empty-data and load-error states are intentional and understandable.

### Ownership validation

- Confirm Designer-owned styling remains in `app/styles.css`.
- Confirm Coder-owned structure, data, and launch configuration remain in their assigned files.
- Confirm no unrelated files are modified during implementation.

## Open Questions

1. Which local preview mechanism and port are preferred for `.vscode/launch.json` if the Codespace exposes more than one supported option?
2. Should the dashboard include filtering, sorting, or search in this iteration, or should it remain a read-only card overview?
3. What exact status and priority vocabulary should be standardized beyond the sample values?
4. Should the contributor-friendly summary use a dedicated `summary` field in the JSON schema, or should the implementation derive it from another field?
5. Is a project count or aggregate status summary required in the header, or is the card grid sufficient for the initial release?
6. Are there branding colors, fonts, or existing product patterns that should replace the Designer's default visual system?

Until these questions are answered, use a simple read-only dashboard, a dedicated `summary` field, a small set of deterministic status and priority values, and a neutral professional visual theme.
