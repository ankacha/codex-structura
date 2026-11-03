# Codex Structura

**Standards timeline and lineage explorer for historic British structural codes. Current version: v2.1 "Guide".**

Codex Structura helps structural engineers working with existing structures find which British standards and codes of practice were in force when a structure was designed. It also traces how each one was revised, replaced or withdrawn. The aim is to make the reuse of existing structures easier, by showing quickly which design basis applied in a given year.

> **Always verify.** This is a research aid. Confirm any date, status or replacement against the [BSI catalogue (BSI Knowledge)](https://knowledge.bsigroup.com/) or the published standard before relying on it.

---

## Features

- **Search**: jump to any standard by designation, title or keyword (`BS 449`, `CP 114`, `steel bridges`).
- **Timeline**: every standard is drawn as a bar from publication to withdrawal. Lanes can be grouped by ICS group, ICS sub-group, industry sector or status, and bars coloured by status or category.
- **Filters**: text, date range (published within, or in force during), status, ICS category tree and industry sector.
- **In force on**: click the year axis, or tick *In force on*, to show only the standards current in a chosen year, e.g. the year a building was designed.
- **Lineage graph**: shows what a standard replaced and what replaced it. *Direct line* shows predecessors and successors only. *Whole family* shows every connected branch. *Infer editions* links consecutive editions that share a designation where the data has no explicit link.
- **Details panel**: the full record for the selected standard, with links to its predecessors and successors.
- **Report builder**: add standards to a basket with your notes and project details, then print to PDF, copy into Word, or export as Markdown, standalone HTML or a CSV reference list. Reports include lineage diagrams and construction-year checks.
- **Shareable links**: the page address carries the selected standard's BSI ID.
- **Light and dark themes**, styled to match the rest of the Pusher family of apps (Frame Pusher, Arch Pusher and the others).

## Reading the timeline

| Bar end | Meaning |
|---|---|
| Solid end | Recorded withdrawal date |
| Dashed end | End taken from the publication date of the replacement |
| Fading end | Withdrawn, but no withdrawal date recorded |
| Reaches the right edge | Still current |

In the lineage graph, each arrow means "was replaced by". Dashed links are inferred editions, and dashed boxes are documents that are not in the dataset.

## Keyboard shortcuts

| Key | Action |
|---|---|
| `/` | Search |
| `F` | Fit the timeline |
| `L` | Zoom to the selected lineage |
| `R` | Add the selected standard to the report |
| `?` | Open the quick guide |
| `Esc` | Close the guide, About or Report |
| Drag | Pan the timeline |
| `Ctrl`/`⌘` + scroll, or pinch | Zoom |
| `Shift` + scroll | Pan sideways |

## Data

The app ships with an embedded dataset of about 4,050 records exported from the BSI catalogue (BSI Knowledge). The data date is shown in the quick guide and on the About page.

You can load a different dataset with **Load CSV** in the top bar. The CSV must use the same columns:

```
BSI_ID, Designation, Title, Status, Replaced by, Replaces, ICS Classifications,
Abstract, Publication date, Confirmation date, Withdrawn on, Amended by,
Descriptors, International relationships, National Committee,
International Committee, Standard Industry Sector, Notes, Alternate numbers,
Author, Affects
```

`Replaced by` and `Replaces` hold BSI IDs, and these build the lineage graph. **Export** downloads the currently filtered list as CSV.

### Limitations

- Amendments are not modelled. Check the amendment history in the record and in the BSI catalogue.
- "In force" means published on or before the chosen year and not withdrawn before it.
- Some records have no recorded withdrawal date or only an approximate publication date. These are flagged in the timeline and on the About page.

## Running it

Codex Structura is a single self-contained `index.html` with no build step and no dependencies. The data is embedded in the page.

- **Locally:** open `index.html` in any modern browser.
- **GitHub Pages:** commit `index.html` to the repository root (or `/docs`), then turn on Pages under *Settings → Pages* for that branch and folder.

Preferences (theme, whether the guide opens on start) and the report basket are stored in the browser's `localStorage` under keys prefixed `cs.`.

## Version history

| Version | Changes |
|---|---|
| v2.1 "Guide" (3 Nov 2026) | Welcome guide restyled to match Frame Pusher: an illustrated, six-step quick guide in a dialog over the app, with a shortcut strip. Light mode fix: selected segmented buttons (Published / In force) keep their highlight and readable text, and all selected buttons share one style in both themes. |
| v2.0 (31 Oct 2026) | Welcome and About pages, version and data stamps, report builder (PDF, Word, Markdown, HTML, CSV) with lineage diagrams and construction-year checks, copyable references, adding filtered sets to the report. |
| v1.0 | Timeline with ICS, date, status and sector filters; lineage graph; inferred editions; details panel; CSV load and export. |

## Disclaimer

Codex Structura is a research aid, not an authoritative source. Dates, statuses and replacement links come from catalogue data, which can be incomplete or wrong. Always confirm against the BSI catalogue or the published standard before using any of it in design, assessment or a calculation pack.
