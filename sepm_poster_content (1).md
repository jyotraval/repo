# SEPM Chart-Paper Poster Content — Hand-Writing Reference

This document contains the **full textual content** AND the **Mermaid diagram code** for both A3 chart-paper posters (Contest Unify and RepoViz). You can:

- **Read** the text below to understand what to hand-write onto your physical chart paper.
- **Render** the Mermaid code in any Mermaid viewer (e.g., [mermaid.live](https://mermaid.live), VS Code with Mermaid extension, GitHub README preview, or the included PNG renders) to see the activity diagram visually.
- **Hand-draw** the activity diagram by copying from either the Mermaid render OR the included PNG preview files.

**Roll No:** 23BIT131
**Subject:** SEPM (23IC401P)
**Division:** 01
**Semester:** 5
**Guide:** Course Faculty

**Companion files** (in same directory):
- `poster_1_contest_unify_preview.png` — full A3 poster preview (Contest Unify)
- `poster_2_repoviz_preview.png` — full A3 poster preview (RepoViz)
- `contest_unify_mermaid.png` — Mermaid-rendered activity diagram (Contest Unify)
- `repoviz_mermaid.png` — Mermaid-rendered activity diagram (RepoViz)

---

# POSTER 1 — ContestUnify

## Title (top of poster, purple bubble font)

```
ContestUnify — The Unified Contest Dashboard
```

Subtitle (below the title, smaller italic):

```
an Activity Diagram for contest aggregation + AI insights
```

## Student Info (far-left vertical strip, rotated 90°)

```
Name: 23BIT131 Student
Roll No: 23BIT131
Div: 01
Sub: SEPM (23IC401P)
Sem: 5
Guide: Course Faculty
```

## AIM (left column, green underlined heading)

```
The aim of this Activity Diagram is to illustrate the end-to-end process of the
Contest Unify platform — how upcoming and live contests are aggregated from
multiple external platforms (Codeforces, LeetCode, CodeChef), cached in
Supabase, displayed on a unified dashboard, and how a student-supplied
Codeforces handle flows through the Gemini 1.5 Flash chatbot to produce AI
performance insights.
```

## Problem Statement (left column, green underlined heading)

```
Designing an automated system Contest Unify to fetch contest metadata from
multiple competitive-programming APIs, normalise formats, store in a cloud
database, and display role-based views (upcoming vs live contests) on a
single dashboard — while integrating a Google Gemini 1.5 Flash chatbot for
Codeforces-handle-based performance analysis, handling API errors, and
ensuring data freshness & insight persistence.
```

## Scope (left column, green underlined heading)

```
Covers: contest aggregation, caching, dashboard display, AI insight
retrieval, and insight history persistence. Out of scope: user
authentication, payment gateways, and integration with external
learning-management systems.
```

## Activity Diagram — Contest Unify (right column)

### Mermaid Diagram Code

Paste this into [mermaid.live](https://mermaid.live) or any Mermaid viewer to render the diagram. It's also pre-rendered as `contest_unify_mermaid.png` in this directory.

```mermaid
flowchart TD
    Start([Start]) --> Open[Student opens ContestUnify]
    Open --> Load[Load cached contests from Supabase]
    Load --> Fresh{Cache fresh?<br/>TTL < 5 min?}

    Fresh -- Yes --> Display[Display upcoming and live contests]
    Fresh -- No --> Fetch[Fetch from Codeforces,<br/>LeetCode, CodeChef APIs]

    Fetch --> FCF[Fetch CF]
    Fetch --> FLC[Fetch LC]
    Fetch --> FCC[Fetch CC]
    FCF --> Norm[Normalise metadata]
    FLC --> Norm
    FCC --> Norm
    Norm --> Store[Store / update Supabase]
    Store --> Display

    Display --> UseAI{Use AI chatbot?}
    UseAI -- No --> Browse[Browse more contests]
    UseAI -- Yes --> Handle[Enter Codeforces handle]

    Handle --> Valid{Handle valid?}
    Valid -- No --> Err1["Show 'invalid handle' error"]:::error
    Err1 -. retry .-> Handle
    Valid -- Yes --> Gemini[Send handle and prompt<br/>to Gemini 1.5 Flash]

    Gemini --> ApiOk{Gemini API ok?}
    ApiOk -- No --> Err2[Log error and retry with backoff]:::error
    Err2 -. retry .-> Gemini
    ApiOk -- Yes --> Feedback[Receive AI performance feedback]

    Feedback --> Save[Save insight to Insight History DB]
    Save --> DispAI[Display AI Insights]
    DispAI --> More{More queries?}
    More -- Yes --> A((A))
    A -. next query .-> Handle
    More -- No --> End([End]):::errorEnd

    classDef error fill:#fde7e7,stroke:#b32121,stroke-width:1.4px,color:#b32121
    classDef errorEnd fill:#fde7e7,stroke:#b32121,stroke-width:1.4px,color:#b32121
```

### Node-by-Node Flow (for hand-drawing)

**Phase 1 — Init & Cache**

1. **[Oval]** `Start` (purple ink, top-left)
   ↓
2. **[Rectangle]** `Student opens ContestUnify`
   ↓
3. **[Rectangle]** `Load cached contests from Supabase`
   ↓
4. **[Diamond]** `Cache fresh? (TTL < 5 min)`
   - **Yes branch** → arrow goes RIGHT to node 9 (Display dashboard)
   - **No branch** → arrow goes DOWN to node 5

5. **[Rectangle, shaded]** `Fetch from Codeforces, LeetCode, CodeChef APIs`
   ↓ (fans out into 3 parallel boxes)
   - **[Rectangle]** `Fetch CF` (Codeforces)
   - **[Rectangle]** `Fetch LC` (LeetCode)
   - **[Rectangle]** `Fetch CC` (CodeChef)

   All 3 merge into ↓

6. **[Rectangle]** `Normalise metadata`
   ↓
7. **[Rectangle]** `Store / update Supabase`
   ↓ (then arrow goes UP-RIGHT to node 9)

8. (Path converges here with the Yes branch from node 4)

9. **[Rounded rectangle, green]** `Display upcoming & live contests`
   ↓

**Phase 2 — AI Insight**

10. **[Diamond]** `Use AI chatbot?`
    - **No branch** → arrow goes RIGHT to node 11 (Browse more contests)
      - 11. **[Rectangle]** `Browse more contests` (terminal — student continues browsing)
    - **Yes branch** → arrow goes DOWN to node 12

12. **[Rectangle]** `Enter Codeforces handle`
    ↓
13. **[Diamond]** `Handle valid?`
    - **No branch** → arrow goes RIGHT to node 14 (error)
      - 14. **[Red Rectangle]** `Show "invalid handle" error`
      - Then **red curved arrow** loops back UP to node 12 (Enter handle) — student retries
    - **Yes branch** → arrow goes DOWN to node 15

15. **[Rectangle, shaded]** `Send handle + prompt to Gemini 1.5 Flash`
    ↓
16. **[Diamond]** `Gemini API ok?`
    - **No branch** → arrow goes RIGHT to node 17 (error)
      - 17. **[Red Rectangle]** `Log error + retry with backoff`
      - Then **red curved arrow** loops back UP to node 15 (Send to Gemini) — retry with backoff
    - **Yes branch** → arrow goes DOWN to node 18

18. **[Rectangle]** `Receive AI performance feedback`
    ↓ (arrow goes LEFT to node 19)

19. **[Rectangle]** `Save insight to Insight History (DB)`
    ↓
20. **[Rounded rectangle, green]** `Display AI Insights`
    ↓

**Phase 3 — Loop / End**

21. **[Diamond]** `More queries?`
    - **Yes branch** → arrow goes RIGHT to **[Circle with "A" inside]** (connector A), then curves UP to node 12 (Enter handle) — student starts next query
    - **No branch** → arrow goes DOWN to node 22

22. **[Red Oval]** `End`

### Phase Labels (right margin, small text)

```
Phase 1 — Init & Cache
(lines from Start to Display Contests)

Phase 2 — AI Insight
(handle → Gemini → save → display)

Phase 3 — Loop / End
```

## Conclusion (far-right vertical strip, rotated 90°)

```
The activity diagram for Contest Unify visualises the automated
contest-aggregation & AI-insight flows — fetching contest metadata
from multiple platform APIs, caching in Supabase, displaying the
unified dashboard, routing the student's Codeforces handle through
Gemini, persisting insights, and looping back for the next query.
It ensures efficient data management, error resilience (invalid-
handle & API-failure retries), and role-free student access to AI
performance feedback.
```

---

# POSTER 2 — RepoViz

## Title (top of poster, purple bubble font)

```
RepoViz — The Python Code Visualizer
```

Subtitle (below the title, smaller italic):

```
an Activity Diagram for the 4-stage parsing & graph pipeline
```

## Student Info (far-left vertical strip, rotated 90°)

```
Name: 23BIT131 Student
Roll No: 23BIT131
Div: 01
Sub: SEPM (23IC401P)
Sem: 5
Guide: Course Faculty
```

## AIM (left column, green underlined heading)

```
The aim of this Activity Diagram is to illustrate the end-to-end process of
the RepoViz pipeline — how a Python project path supplied on the command
line is scanned for .py files, parsed via the AST module into CodeElement
instances, transformed into a NetworkX directed graph with import-resolved
call edges, and finally rendered through Graphviz into PNG / SVG / DOT
output files.
```

## Problem Statement (left column, green underlined heading)

```
Designing an automated tool RepoViz to scan any Python codebase, extract
classes / functions / methods / module-level code, resolve import aliases,
build a directed call graph, and render hierarchical visualisations
(hybrid / flow / simple / standard styles) — while respecting ignore
patterns (venv, tests), detecting entry points, and supporting multiple
output formats.
```

## Scope (left column, green underlined heading)

```
Covers: CLI parsing, recursive .py file discovery, AST extraction,
alias resolution, NetworkX graph construction, and Graphviz rendering.
Out of scope: cross-language projects, runtime call profiling, and
live editor integration.
```

## Activity Diagram — RepoViz (right column)

### Mermaid Diagram Code

Paste this into [mermaid.live](https://mermaid.live) or any Mermaid viewer to render the diagram. It's also pre-rendered as `repoviz_mermaid.png` in this directory.

```mermaid
flowchart TD
    Start([Start]) --> CLI["Parse CLI args<br/>project_path, --ignore,<br/>--format, --output"]
    CLI --> Valid{project_path valid?}

    Valid -- No --> Err1["Print usage error to stderr"]:::error
    Err1 --> Exit1([Exit 1]):::errorEnd
    Valid -- Yes --> Stage1["Stage 1 - File Scanner<br/>Recursively discover .py files,<br/>apply --ignore patterns"]

    Stage1 --> Files{Files found?}
    Files -- No --> Err2["Print 'no .py files found' + exit"]:::error
    Err2 --> Exit2([Exit 1]):::errorEnd
    Files -- Yes --> Stage2["Stage 2 - AST Parser<br/>Parse each .py file via Python ast module"]

    Stage2 --> Extract["Extract CodeElement instances<br/>file, class, function, method, module"]
    Extract --> More{More files?}
    More -- Yes --> B((B))
    B -. next file .-> Stage2
    More -- No --> Stage3["Stage 3 - Graph Builder<br/>Build NetworkX DiGraph,<br/>resolve import aliases"]

    Stage3 --> Edges["Add directed call edges<br/>caller to callee, detect __main__ entry points"]
    Edges --> Stage4["Stage 4 - Visualizer<br/>Choose style: hybrid / flow / simple / standard,<br/>call Graphviz"]

    Stage4 --> Fmt{Output format?}
    Fmt -- png --> RPNG[Render PNG]
    Fmt -- svg --> RSVG[Render SVG]
    Fmt -- both/all --> RALL[PNG + SVG + DOT]
    RPNG --> SPNG[Save PNG file]
    RSVG --> SSVG[Save SVG file]
    RALL --> SDOT[Save DOT file]

    SPNG --> A((A))
    SSVG --> A
    SDOT --> A
    A --> SaveAll["Save output file(s) to disk"]
    SaveAll --> Stats["Print statistics<br/>files, classes, functions, connections"]
    Stats --> End([End])

    classDef error fill:#fde7e7,stroke:#b32121,stroke-width:1.4px,color:#b32121
    classDef errorEnd fill:#fde7e7,stroke:#b32121,stroke-width:1.4px,color:#b32121
```

### Node-by-Node Flow (for hand-drawing)

**Phase 1 — CLI & Init**

1. **[Oval]** `Start` (top-left)
   ↓
2. **[Rectangle]** `Parse CLI args (project_path, --ignore, --format, --output)`
   ↓
3. **[Diamond]** `project_path valid?`
   - **No branch** → arrow goes RIGHT to node 4 (error)
     - 4. **[Red Rectangle]** `Print usage error to stderr`
        ↓
     - 5. **[Red Oval]** `Exit (1)`
   - **Yes branch** → arrow goes DOWN to node 6

**Phase 2 — Scan & AST (file loop)**

6. **[Rectangle, shaded]** `Stage 1 — File Scanner` (header: `Recursively discover .py files, apply --ignore patterns`)
   ↓
7. **[Diamond]** `Files found?`
   - **No branch** → arrow goes RIGHT to node 8 (error)
     - 8. **[Red Rectangle]** `Print "no .py files found" + exit`
        ↓
     - 9. **[Red Oval]** `Exit (1)`
   - **Yes branch** → arrow goes DOWN to node 10

10. **[Rectangle, shaded]** `Stage 2 — AST Parser` (header: `Parse each .py file via Python ast module`)
    ↓
11. **[Rectangle]** `Extract CodeElement instances (file, class, function, method, module)`
    ↓
12. **[Diamond]** `More files?`
    - **Yes branch** → arrow goes LEFT through **[Circle with "B" inside]** (connector B), then curves UP back to node 10 (Stage 2 AST Parser) — loop processes next file
    - **No branch** → arrow goes DOWN to node 13

**Phase 3 — Graph Build**

13. **[Rectangle, shaded]** `Stage 3 — Graph Builder` (header: `Build NetworkX DiGraph; resolve import aliases`)
    ↓
14. **[Rectangle]** `Add directed call edges (caller → callee); detect __main__ entry points`
    ↓ (arrow goes RIGHT to Phase 4)

**Phase 4 — Render & Save**

15. **[Rectangle, shaded]** `Stage 4 — Visualizer` (header: `Choose style (hybrid / flow / simple / standard); call Graphviz`)
    ↓
16. **[Diamond]** `Output format?`
    - **png branch** → arrow goes UP-RIGHT to node 17
    - **svg branch** → arrow goes RIGHT to node 18
    - **both/all branch** → arrow goes DOWN-RIGHT to node 19

17. **[Rectangle]** `Render PNG`
    ↓
18. **[Rectangle]** `Render SVG`
    ↓ (alongside)
19. **[Rectangle]** `PNG+SVG+DOT` (for both/all case)

20. **[Rectangle]** `Save PNG file` (below node 17)
21. **[Rectangle]** `Save SVG file` (below node 18)
22. **[Rectangle]** `Save DOT file` (below node 19)

All three Save boxes converge into ↓

23. **[Circle with "A" inside]** (connector A — merge point)
    ↓
24. **[Rectangle]** `Save output file(s) to disk`
    ↓ (arrow goes UP)
25. **[Rectangle]** `Print statistics (files, classes, functions, connections)`
    ↓
26. **[Oval]** `End`

### Phase Labels (right margin, small text)

```
Phase 1 — CLI & Init
(parse + validate path)

Phase 2 — Scan & AST
(file loop)

Phase 3 — Graph Build

Phase 4 — Render & Save
(format branch)
```

## Conclusion (far-right vertical strip, rotated 90°)

```
The activity diagram for RepoViz visualises the automated 4-stage
pipeline — CLI parsing & path validation, recursive .py discovery
with ignore patterns, AST extraction of CodeElements, NetworkX
graph construction with import-alias resolution, and Graphviz
rendering of PNG / SVG / DOT output files. It ensures efficient
code-structure analysis, graceful error handling (invalid path,
no files, format errors), and flexible output-format selection
for visualising any Python project.
```

---

# Hand-Writing Tips

## Materials

- **A3 white chart paper**, landscape orientation
- **Green marker** for the decorative border + section headings (AIM, Problem Statement, Scope, Conclusion)
- **Purple / dark violet pen** for body text, the title, and the activity-diagram outlines
- **Red pen** for error paths, "No" branch labels, error boxes, and Exit ovals
- **Pencil** (optional) for light shading inside 1-2 highlighted process boxes
- **Ruler** for clean rectangle/diamond outlines (or freehand for a more hand-drawn feel)
- **Compass or circular template** for the Start/End ovals and the circled-letter connectors

## Layout Sketch (before you start writing)

```
+--------------------------------------------------------------+
| [gold tape corner]                              [gold tape]   |
|   +-----+ -----------------------------------------+ -----+   |
|   |  S  |        TITLE (purple bubble font)        |  C  |   |
|   |  t  |------------------------------------------|  o  |   |
|   |  u  |              |                          |  n  |   |
|   |  d  |   AIM        |                          |  c  |   |
|   |  e  |   _______    |     ACTIVITY DIAGRAM     |  l  |   |
|   |  n  |              |                          |  u  |   |
|   |  t  |   Problem    |                          |  s  |   |
|   |     |   Statement  |                          |  i  |   |
|   |  I  |              |                          |  o  |   |
|   |  n  |   Scope      |                          |  n  |   |
|   |  f  |              |                          |     |   |
|   |  o  |              |                          |     |   |
|   +-----+--------------+--------------------------+ -----+   |
| [gold tape]                                      [gold tape] |
+--------------------------------------------------------------+
```

- Far-left vertical strip: Student Info (rotated 90°)
- Top header band: Title (purple, large) + subtitle
- Left text column: AIM → Problem Statement → Scope (each with green underlined heading)
- Right diagram column: Activity Diagram (SVG-style with ovals, rectangles, diamonds)
- Far-right vertical strip: Conclusion (rotated 90°)
- Decorative green border around the entire perimeter
- Optional gold/yellow washi-tape corners

## Drawing the Activity Diagram

1. **Start with the Start oval** at the top-left of the diagram column.
2. **Draw the main vertical spine** going down — boxes connected by arrows.
3. **Branch out** for each diamond decision (Yes usually continues down, No usually goes right to an error box).
4. **Use red pen** for:
   - "No" branch labels
   - Error rectangles (`Show "invalid handle" error`, `Log error + retry`, `Print usage error`, `Print "no .py files found" + exit`)
   - Exit ovals (`Exit (1)`, `End` if reached via error)
5. **Use green pen** for:
   - Section headings (AIM, Problem Statement, Scope, Conclusion)
   - The decorative border
   - "Yes" branch labels (optional — green or just normal ink)
6. **Draw circled-letter connectors** as small circles with a single capital letter inside:
   - Poster 1 (Contest Unify): `[A]` at the loop-back from "More queries?" to "Enter handle"
   - Poster 2 (RepoViz): `[A]` at the merge point of the three Save boxes; `[B]` on the loop-back from "More files?" to "Stage 2 AST Parser"
7. **Label every arrow** with Yes / No on decision branches (Yes green, No red).
8. **Optional shading**: lightly shade 1-2 important process boxes with pencil (e.g., "Fetch from Codeforces/LeetCode/CodeChef APIs" in Poster 1, "Stage 2 — AST Parser" in Poster 2).

## How to Use the Mermaid Code

The Mermaid code blocks above let you render the activity diagram in any Mermaid viewer. Here's how:

### Option A: Online Mermaid Live Editor (easiest)

1. Go to <https://mermaid.live>
2. Delete the default code in the left panel
3. Paste the Mermaid code from this file (the part between ` ```mermaid ` and ` ``` `)
4. The diagram will render instantly on the right
5. Click "Actions" → "PNG" or "SVG" to download

### Option B: VS Code

1. Install the "Markdown Preview Mermaid Support" extension
2. Open this `.md` file in VS Code
3. Press `Ctrl+Shift+V` to open Markdown preview — the Mermaid blocks render inline

### Option C: GitHub

If you push this `.md` file to a GitHub repo, GitHub will render the Mermaid blocks automatically when you view the file on the web.

### Option D: Use the pre-rendered PNGs

This directory already contains the rendered Mermaid diagrams as PNGs:

- `contest_unify_mermaid.png` — Contest Unify activity diagram (1752 × 2302)
- `repoviz_mermaid.png` — RepoViz activity diagram (1752 × 2230)

Open them in any image viewer to see the diagrams without needing to render anything yourself.

## Final Checklist (before you submit)

- [ ] Green decorative border around all 4 edges
- [ ] Title in purple bubble font at the top
- [ ] Student info strip on far-left (vertical, rotated 90°) — Name, Roll No (23BIT131), Div, Sub, Sem, Guide
- [ ] AIM section with green underlined heading + paragraph
- [ ] Problem Statement section with green underlined heading + paragraph
- [ ] Scope section with green underlined heading + paragraph
- [ ] Activity diagram on the right with:
  - [ ] Start oval at the top
  - [ ] Process rectangles (with the exact labels from the node list above)
  - [ ] Decision diamonds (with Yes/No branch labels)
  - [ ] Red error paths and error rectangles
  - [ ] Circled-letter connectors ([A], [B])
  - [ ] End oval at the bottom
  - [ ] All arrows clearly directional
- [ ] Conclusion section on far-right (vertical, rotated 90°) with heading + paragraph
- [ ] Overall hand-drawn aesthetic (single-weight pen strokes, slightly imperfect lines OK)

## Choose Your Poster

You have two complete content sets above. Pick the one you prefer:

- **Contest Unify** — focuses on contest aggregation + AI insights (Gemini chatbot). Good if you want to highlight external API integration, caching, and AI/ML.
- **RepoViz** — focuses on the 4-stage code-visualization pipeline (CLI → scan → AST → graph → render). Good if you want to highlight a clean pipeline architecture with multiple output formats.

Both follow the same structure and visual style. Pick one and hand-draw it. The reference HTML posters (in `poster_1_contest_unify_preview.png` and `poster_2_repoviz_preview.png`) give you the visual layout to copy, and the Mermaid renders (in `contest_unify_mermaid.png` and `repoviz_mermaid.png`) give you clean activity diagrams to copy node-by-node.

Good luck with your chart paper!
