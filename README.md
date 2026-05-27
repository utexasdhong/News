# News

A monthly, curated digest of the most significant news. Each month is a folder; each subcategory is one markdown file with 3–5 hand-picked stories and source links.

This is a reading aid. Quality over volume.

🌐 **Live site:** https://utexasdhong.github.io/News/

## Layout

```
.
├── docs/                       # site content (rendered by MkDocs)
│   ├── index.md                # homepage
│   ├── 2026-01/                # one folder per month
│   │   ├── index.md            # month landing page
│   │   ├── Technology/
│   │   │   ├── AI/             # Models, Research, Industry, Products-Agents, Policy-Safety
│   │   │   ├── Hardware-Chips.md
│   │   │   └── Cybersecurity.md
│   │   ├── Politics/           # US, International
│   │   ├── Science/            # Space, Health-Medicine, Climate
│   │   ├── Business-Economy/   # Markets-Macro, Crypto-Fintech
│   │   ├── World/              # Major-Events
│   │   └── Culture/            # Notable
│   └── 2026-{02..05}/          # same structure
├── meta/                       # spec + plan (not rendered)
│   ├── specs/
│   └── plans/
├── mkdocs.yml                  # site config (Material for MkDocs)
└── .github/workflows/deploy.yml
```

## Months covered

- 2026-01
- 2026-02
- 2026-03
- 2026-04
- 2026-05 (partial — through 2026-05-26)

## Story format

Each subcategory file uses this template:

```markdown
## 1. [Headline](https://source.url)
**Source:** Outlet · **Date:** YYYY-MM-DD

Why this matters: 1–2 sentence note on real-world significance.
```

## Sourcing rules

- Authoritative outlets first: Reuters, AP, Bloomberg, FT, NYT, WSJ for general news; Nature, Science, NEJM for science; MIT Tech Review, Ars Technica, The Verge, IEEE Spectrum for tech.
- "Significant" = real-world impact, not hype. Multi-outlet coverage is a useful signal.
- Prefer free links when a free alternative to a paywalled source exists.
- No speculation pieces as headline stories.

## Refreshing for a new month

Ask Claude to "build the news digest for `YYYY-MM`". Convention:

1. Create `docs/YYYY-MM/` with the full subcategory tree (mirror an existing month).
2. Curate per the sourcing rules above.
3. Add the new month to `mkdocs.yml` nav (top of the list — reverse chronological).
4. Add the new month to the "Months covered" list in this README and to the homepage grid.
5. Commit + push — the site rebuilds automatically.

## Building the site locally (optional)

```bash
pip install mkdocs-material
mkdocs serve
```

Then open `http://localhost:8000`.

## References

- Design spec: [`meta/specs/2026-05-26-news-curation-design.md`](meta/specs/2026-05-26-news-curation-design.md)
- Backfill plan: [`meta/plans/2026-05-26-news-curation-backfill.md`](meta/plans/2026-05-26-news-curation-backfill.md)
