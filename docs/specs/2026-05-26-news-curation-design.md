# News Curation System — Design

**Date:** 2026-05-26
**Owner:** Dillan

## Purpose

A monthly-refreshable, curated digest of the most significant news, organized by category. Each month gets its own folder; each subcategory gets a markdown file with 3–5 hand-picked stories and links to read in full.

This is a reading aid, not an aggregator. Quality over volume.

## Scope

- **Backfill:** January 2026 through May 2026 (5 months).
- **Going forward:** Re-runnable monthly. The structure is the same every month so it can be regenerated on demand.

## Folder Structure

```
C:\Vibecoding\News\
├── README.md
├── docs/specs/                       # this design lives here
├── 2026-01/
│   ├── Technology/
│   │   ├── AI/
│   │   │   ├── Models.md
│   │   │   ├── Research.md
│   │   │   ├── Industry.md
│   │   │   ├── Products-Agents.md
│   │   │   └── Policy-Safety.md
│   │   ├── Hardware-Chips.md
│   │   └── Cybersecurity.md
│   ├── Politics/
│   │   ├── US.md
│   │   └── International.md
│   ├── Science/
│   │   ├── Space.md
│   │   ├── Health-Medicine.md
│   │   └── Climate.md
│   ├── Business-Economy/
│   │   ├── Markets-Macro.md
│   │   └── Crypto-Fintech.md
│   ├── World/
│   │   └── Major-Events.md
│   └── Culture/
│       └── Notable.md
├── 2026-02/   (same structure)
├── 2026-03/
├── 2026-04/
└── 2026-05/
```

## Per-Story Format

Each `.md` file uses this template:

```markdown
# <Subcategory> — <Month YYYY>

## 1. [Headline](https://source.url)
**Source:** <Outlet> · **Date:** YYYY-MM-DD

Why this matters: 1–2 sentence note on significance.

## 2. ...
```

- Target: **3–5 stories per subcategory.**
- If a subcategory had a quiet month, ship fewer strong stories rather than padding. Note "slim month" at the top of the file when this happens.

## Sourcing Rules

- **Authoritative outlets first.** General: Reuters, AP, Bloomberg, FT, NYT, WSJ. Science: Nature, Science, NEJM. Tech: MIT Tech Review, Ars Technica, The Verge, IEEE Spectrum.
- **"Significant" means real-world impact, not hype.** Multi-outlet coverage is a useful signal, not a requirement.
- **Prefer free links** when a free alternative to a paywalled source exists.
- **No speculation pieces** as headline stories. Opinion/analysis is fine as supporting context inside the "Why this matters" line.

## Execution Plan

1. Scaffold folder skeleton + README.
2. **Pilot: build January 2026 in full.** User reviews format and curation taste.
3. On approval, fan out **February through May 2026 in parallel** (one subagent per month — they're independent).
4. Final pass: ensure every file follows the template, no broken links, no padding.

## Re-Run Convention (Future Months)

To generate the next month, the operator (Claude or human):
1. Creates `YYYY-MM/` folder under `News/` with the full subcategory tree.
2. Curates per the sourcing rules above.
3. Updates the README's "Months covered" list.

The README will document this so future-me has the convention written down.

## Non-Goals

- Not a real-time news feed.
- Not a comprehensive archive — only the *most significant* stories.
- Not editorial commentary — "Why this matters" is one factual sentence about impact, not opinion.
- Not auto-refreshing — the user (or Claude on request) runs the refresh.

## Open Questions

None at design time. Subcategory list can evolve based on what feels useful after a few months.
