# Codex Structura

**v2.3 "Integrity"** · A timeline and lineage explorer for historic British structural standards and codes of practice.

Codex Structura helps structural engineers who are assessing, adapting and reusing existing structures. It shows which British Standards and Codes of Practice were in force when a building was designed and built, and how each one was revised, replaced or withdrawn afterwards.

Live site: <https://ankacha.github.io/>

> **Always verify.** Codex Structura is a research aid, not an authoritative source. Its data is an export of the BSI catalogue taken at one point in time, and it can contain gaps, transcription errors and status changes made after the export. Before you rely on a designation, edition, publication or withdrawal date, amendment or replacement in a design, assessment, calculation pack or report, confirm it against the [BSI catalogue (BSI Knowledge)](https://knowledge.bsigroup.com/) or the published document. Codex Structura is not affiliated with or endorsed by BSI.

---

## Features

### Timeline
- Each standard is a bar that runs from its publication date to its withdrawal date. The bar's colour shows its status: current, superseded or withdrawn.
- How a bar ends tells you how reliable its end date is:
  - a solid end is a recorded withdrawal;
  - a dashed end is inferred from the date the replacement was published;
  - a fading end means no date is known.
- Lanes group standards by ICS group, ICS sub-group, industry sector or status, or put everything in a single lane. Bars can be coloured by status or by category.
- A histogram of publications runs along the year axis. Drag along the axis to select a range of years, or click it to see what was in force in a single year.

### Filters
- **Text filter:** every word must match the designation, title, abstract or descriptors. It uses fuzzy matching unless you turn it off.
- **Dates:** filter by *Published* within a range, or *In force* at any time within it. **In force on** shows a single year, such as a construction year.
- **Status**, **ICS category tree** (with counts) and **industry sector**.
- **Lineage & data checks:** show only the standards flagged by one of the checks below.

### Lineage graph
- Shows predecessors and successors of the selected standard. **Direct line** shows only its ancestors and descendants; **Whole family** shows every standard connected to it through any replacement link.
- **Infer editions** (optional, drawn dashed) links consecutive editions that share a designation, such as BS 449:1948 → BS 449:1959, where the data records no link between them.
- Documents referenced in the data but missing from the export appear as dashed "not in dataset" boxes.
- Badges mark **merges**, **splits** and **dead ends**. Edges carry labels for **gaps**, **⇆ overlaps** and **one-sided** links.

### Lineage & data checks (new in v2.3)
The **Checks** page runs nine checks over the dataset. Each check comes with a list you can click through, a CSV export and, where it applies, a *Show on timeline* filter.

| Check | Meaning |
|---|---|
| Merges | Replaces two or more standards. |
| Splits | Replaced by two or more standards. |
| Dead ends | Withdrawn or superseded with no recorded or inferred successor. |
| One-sided links | The link appears on only one of the two records ("Replaced by" without the matching "Replaces", or the reverse). |
| Coverage gaps | The predecessor was withdrawn more than 6 months before the successor was published. |
| Transition overlaps | The successor was published more than 6 months before the predecessor was withdrawn, so either could have been used. |
| Date order | The successor is dated earlier than the standard it replaces. |
| Orphans | No recorded replacement link in either direction. |
| Missing fields | A core field is empty or contradictory, e.g. no publication date, "superseded" with no successor, or withdrawn before published. |

Each standard's details panel lists its flags in plain language and shows a **record completeness** score.

A flag is a prompt to check, not a finding. Many reflect gaps in the catalogue export, especially before about 1970, and most overlaps are genuine transition periods.

### Fuzzy search (new in v2.3)
The top search box and the text filter fall back to fuzzy matching when a word has no exact match. Fuzzy matching covers:
- word endings, such as *beams* → *beam*;
- close misspellings that occur in the data: one letter off for words of 5 or more letters, two letters off for 8 or more;
- older or alternative terms, such as *steel / steelwork / iron*, *masonry / brickwork*, *column / stanchion* and *beam / girder / joist*.

Fuzzy results are listed after exact ones and marked **≈**. Numbers and designations always match exactly.

### Details, references and reports
- The details panel shows dates, status, sector, committee, BSI ID, amendments, abstract, notes, classification and descriptors, plus links to predecessors and successors.
- **Copy reference** gives a citation for a calculation pack. **Copy link** gives a URL to the selected standard; the URL hash tracks the selected standard, so links can be shared.
- **Report builder:** add standards to a basket with **+ Add to report**, the **R** key, or *Add filtered standards to report*. Then add project details, an assumed construction year and notes. The report checks whether each standard was in force in that year and names the edition that was. Reports can be printed to PDF or exported as Word, Markdown, HTML or CSV, with lineage diagrams included. Every report records the tool version, the date of application and the data date.

### Other
- Light and dark themes, both in the cyberpunk style shared with the author's other apps.
- **Export** downloads the filtered list as CSV, including data-check and completeness columns.
- **Load CSV** loads a different export with the same columns, processed entirely in the browser.
- A welcome guide and an About page covering data provenance, how dates are read, and the version history.
- Preferences such as theme, layout, filters and the report basket are saved in the browser's `localStorage`.

## Keyboard shortcuts

| Key | Action |
|---|---|
| `/` | Focus the search box |
| `F` | Fit the timeline to all years |
| `L` | Zoom the timeline to the selected lineage |
| `R` | Add or remove the selected standard from the report |
| `?` | Open the welcome guide |
| `Esc` | Close a view or panel |

On the timeline and graph: drag to pan, use Ctrl + scroll or pinch to zoom, and Shift + scroll to move sideways.

## Data

The bundled dataset is an export of the BSI catalogue (BSI Knowledge), last updated 31 October 2026, with 4,053 records. It is embedded in `index.html` as JSON in `<script id="data">`.

To use a different dataset, click **Load CSV**. The file needs at least the `BSI_ID` and `Designation` columns; the full export uses:

```
BSI_ID, Designation, Title, Status, Replaced by, Replaces, ICS Classifications, Abstract,
Publication date, Confirmation date, Withdrawn on, Amended by, Descriptors,
International relationships, National Committee, International Committee,
Standard Industry Sector, Notes, Alternate numbers, Author, Affects
```

Notes on parsing:
- **Dates:** formats such as `16-Dec-35`, `1935-12-16`, `16/12/1935` and `1935` are accepted. For two-digit years, a publication year takes the century closest to the year in the designation; a withdrawal or confirmation year takes the first century on or after the publication year.
- **Replacement fields:** these can hold BSI IDs or designations, separated by `|`.
- **ICS classifications:** paths use `>` between levels and `||` between classifications.

## Deployment

Codex Structura is a single self-contained `index.html`: HTML, CSS, JavaScript and data, with no build step and no dependencies. To deploy:

1. Commit `index.html` to the repository.
2. Enable **GitHub Pages** for the branch (Settings → Pages).

To run it locally, open `index.html` in a browser.

### Analytics
The page includes the standard Google Tag Manager container snippet (`GTM-WMK9FHGQ`): the script in `<head>` and the `<noscript>` iframe right after `<body>`. Tags are configured in Tag Manager, not in this file.

## Version history

| Version | Date | Changes |
|---|---|---|
| v2.3 "Integrity" | 9 Nov 2026 | Checks page with nine lineage and data checks and CSV export. Flags and record completeness in the details panel. Merge, split and dead-end badges and gap, overlap and one-sided labels in the graph. Data-check filter. Fuzzy search. Data-check columns in the CSV export. Tag Manager snippet corrected (12 Nov 2026). |
| v2.2 "Home" | 9 Nov 2026 | Home button linking to ankacha.github.io (opens in a new tab when embedded in another page). Google Tag Manager added. |
| v2.1 | 3 Nov 2026 | Welcome guide restyled as an illustrated six-step dialog. Light-mode button styling fixes. |
| v2.0 | 31 Oct 2026 | Welcome and About pages, version and data stamps, report builder, copyable references, adding filtered sets to the report. |
| v1.0 | — | Timeline with ICS, date, status and sector filters. Lineage graph, inferred editions, details panel, CSV load and export. |

## Disclaimer

British Standards are available from BSI. Responsibility for the codes used in any design or assessment stays with the engineer.
