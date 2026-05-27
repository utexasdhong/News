# News Curation Backfill — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Scaffold the `C:\Vibecoding\News\` project and backfill curated, link-driven news digests for January through May 2026.

**Architecture:** Date-keyed folders (`YYYY-MM/`) with a fixed subcategory tree. Each subcategory is one markdown file containing 3–5 hand-picked stories with source links and one-line significance notes. Content is sourced via WebSearch from authoritative outlets. Curation work for distinct months is parallelizable.

**Tech Stack:** Markdown files, Bash for scaffolding, WebSearch/WebFetch for sourcing. No code, no build system, no tests in the traditional sense — verification is per-file format and link sanity.

---

## File Structure

**Created during scaffold (Task 1):**

```
C:\Vibecoding\News\
├── README.md
├── docs/specs/2026-05-26-news-curation-design.md         (already exists)
├── docs/plans/2026-05-26-news-curation-backfill.md       (this file)
├── 2026-01/  (folder tree per spec — empty .md files)
├── 2026-02/
├── 2026-03/
├── 2026-04/
└── 2026-05/
```

**Subcategory tree replicated under every `YYYY-MM/`:**

```
Technology/
├── AI/
│   ├── Models.md
│   ├── Research.md
│   ├── Industry.md
│   ├── Products-Agents.md
│   └── Policy-Safety.md
├── Hardware-Chips.md
└── Cybersecurity.md
Politics/
├── US.md
└── International.md
Science/
├── Space.md
├── Health-Medicine.md
└── Climate.md
Business-Economy/
├── Markets-Macro.md
└── Crypto-Fintech.md
World/
└── Major-Events.md
Culture/
└── Notable.md
```

**13 subcategory files per month × 5 months = 65 content files total.**

---

## Per-File Content Template

Every subcategory file follows this exact template:

```markdown
# <Subcategory> — <Month YYYY>

## 1. [Headline](https://source.url)
**Source:** <Outlet> · **Date:** YYYY-MM-DD

Why this matters: One or two sentences on real-world significance.

## 2. [Headline](https://source.url)
**Source:** <Outlet> · **Date:** YYYY-MM-DD

Why this matters: ...

(continue 3–5 entries)
```

**Slim-month exception:** If a subcategory had fewer than 3 genuinely significant stories, ship 1–2 with a top-of-file note: `> Slim month — only N significant stories found.` Do not pad.

---

## Task 1: Scaffold folder skeleton + empty placeholder files

**Files:**
- Create: `C:\Vibecoding\News\2026-{01..05}\` plus full subcategory tree
- Create: 65 empty `.md` files (13 subcategories × 5 months)

- [ ] **Step 1: Create all directories**

Run in Bash:
```bash
for month in 2026-01 2026-02 2026-03 2026-04 2026-05; do
  mkdir -p "C:/Vibecoding/News/$month/Technology/AI"
  mkdir -p "C:/Vibecoding/News/$month/Politics"
  mkdir -p "C:/Vibecoding/News/$month/Science"
  mkdir -p "C:/Vibecoding/News/$month/Business-Economy"
  mkdir -p "C:/Vibecoding/News/$month/World"
  mkdir -p "C:/Vibecoding/News/$month/Culture"
done
```

- [ ] **Step 2: Create empty placeholder .md files**

Run in Bash:
```bash
for month in 2026-01 2026-02 2026-03 2026-04 2026-05; do
  base="C:/Vibecoding/News/$month"
  touch "$base/Technology/AI/Models.md"
  touch "$base/Technology/AI/Research.md"
  touch "$base/Technology/AI/Industry.md"
  touch "$base/Technology/AI/Products-Agents.md"
  touch "$base/Technology/AI/Policy-Safety.md"
  touch "$base/Technology/Hardware-Chips.md"
  touch "$base/Technology/Cybersecurity.md"
  touch "$base/Politics/US.md"
  touch "$base/Politics/International.md"
  touch "$base/Science/Space.md"
  touch "$base/Science/Health-Medicine.md"
  touch "$base/Science/Climate.md"
  touch "$base/Business-Economy/Markets-Macro.md"
  touch "$base/Business-Economy/Crypto-Fintech.md"
  touch "$base/World/Major-Events.md"
  touch "$base/Culture/Notable.md"
done
```

- [ ] **Step 3: Verify**

Run:
```bash
find "C:/Vibecoding/News" -name "*.md" | wc -l
```
Expected: at least `65` (plus README and spec/plan files when present).

---

## Task 2: Write the README

**Files:**
- Create: `C:\Vibecoding\News\README.md`

- [ ] **Step 1: Write README**

Content of `C:\Vibecoding\News\README.md`:

````markdown
# News

A monthly, curated digest of the most significant news. Each month is a folder; each subcategory is one markdown file with 3–5 hand-picked stories and source links.

This is a reading aid. Quality over volume.

## Layout

```
YYYY-MM/
├── Technology/
│   ├── AI/                  # Models, Research, Industry, Products-Agents, Policy-Safety
│   ├── Hardware-Chips.md
│   └── Cybersecurity.md
├── Politics/                # US, International
├── Science/                 # Space, Health-Medicine, Climate
├── Business-Economy/        # Markets-Macro, Crypto-Fintech
├── World/                   # Major-Events
└── Culture/                 # Notable
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

1. Create `YYYY-MM/` with the full subcategory tree (mirror an existing month).
2. Curate per the sourcing rules above.
3. Add the new month to the "Months covered" list in this README.

Design spec: [`docs/specs/2026-05-26-news-curation-design.md`](docs/specs/2026-05-26-news-curation-design.md)
Backfill plan: [`docs/plans/2026-05-26-news-curation-backfill.md`](docs/plans/2026-05-26-news-curation-backfill.md)
````

- [ ] **Step 2: Verify**

Open `C:\Vibecoding\News\README.md` and confirm:
- Layout section matches the actual folder tree from Task 1.
- "Months covered" lists 2026-01 through 2026-05.
- Story format template is present.

---

## Task 3: Curate January 2026 (pilot — all 13 subcategories)

This is the **pilot** task. The user reviews this month before any other month is built. The format and curation quality demonstrated here become the bar for Feb–May.

**Files (modify the empty placeholders from Task 1):**
- `C:\Vibecoding\News\2026-01\Technology\AI\Models.md`
- `C:\Vibecoding\News\2026-01\Technology\AI\Research.md`
- `C:\Vibecoding\News\2026-01\Technology\AI\Industry.md`
- `C:\Vibecoding\News\2026-01\Technology\AI\Products-Agents.md`
- `C:\Vibecoding\News\2026-01\Technology\AI\Policy-Safety.md`
- `C:\Vibecoding\News\2026-01\Technology\Hardware-Chips.md`
- `C:\Vibecoding\News\2026-01\Technology\Cybersecurity.md`
- `C:\Vibecoding\News\2026-01\Politics\US.md`
- `C:\Vibecoding\News\2026-01\Politics\International.md`
- `C:\Vibecoding\News\2026-01\Science\Space.md`
- `C:\Vibecoding\News\2026-01\Science\Health-Medicine.md`
- `C:\Vibecoding\News\2026-01\Science\Climate.md`
- `C:\Vibecoding\News\2026-01\Business-Economy\Markets-Macro.md`
- `C:\Vibecoding\News\2026-01\Business-Economy\Crypto-Fintech.md`
- `C:\Vibecoding\News\2026-01\World\Major-Events.md`
- `C:\Vibecoding\News\2026-01\Culture\Notable.md`

- [ ] **Step 1: Research January 2026 news per subcategory**

For each subcategory, run targeted WebSearch queries. Example search patterns:

| Subcategory | Example queries |
|---|---|
| Technology/AI/Models | "most significant AI model release January 2026", "GPT Claude Gemini new model January 2026" |
| Technology/AI/Research | "AI research breakthrough January 2026", "machine learning paper January 2026" |
| Technology/AI/Industry | "AI company funding acquisition January 2026", "OpenAI Anthropic news January 2026" |
| Technology/AI/Products-Agents | "AI agent product launch January 2026", "enterprise AI deployment January 2026" |
| Technology/AI/Policy-Safety | "AI regulation January 2026", "AI safety policy January 2026" |
| Technology/Hardware-Chips | "semiconductor chip announcement January 2026", "Nvidia AMD Intel January 2026" |
| Technology/Cybersecurity | "major cyberattack data breach January 2026", "ransomware January 2026" |
| Politics/US | "US politics major news January 2026", "Congress White House January 2026" |
| Politics/International | "international politics major news January 2026", "election news January 2026" |
| Science/Space | "space launch discovery January 2026", "NASA SpaceX January 2026" |
| Science/Health-Medicine | "medical breakthrough drug approval January 2026", "FDA approval January 2026" |
| Science/Climate | "climate change major news January 2026", "climate policy January 2026" |
| Business-Economy/Markets-Macro | "Federal Reserve markets January 2026", "GDP inflation January 2026" |
| Business-Economy/Crypto-Fintech | "Bitcoin crypto major news January 2026", "fintech news January 2026" |
| World/Major-Events | "biggest world news January 2026", "global crisis January 2026" |
| Culture/Notable | "major cultural event January 2026", "Oscar Grammy notable January 2026" |

For each, do 1–3 searches, then if needed WebFetch the most authoritative source to verify date/details. **Confirm the story is actually from January 2026** before including it.

- [ ] **Step 2: Curate 3–5 stories per subcategory**

For each subcategory, select stories using the sourcing rules:
- Authoritative outlets first
- Real-world impact, not hype
- Multi-outlet coverage is a positive signal
- No speculation as headline

If a subcategory has fewer than 3 strong stories, ship 1–2 and add the slim-month note. Do not pad.

- [ ] **Step 3: Write each subcategory file**

For each of the 16 files listed above, write content using the exact template:

```markdown
# <Subcategory> — January 2026

## 1. [Headline](https://source.url)
**Source:** Outlet · **Date:** 2026-01-DD

Why this matters: ...

## 2. [Headline](https://source.url)
**Source:** Outlet · **Date:** 2026-01-DD

Why this matters: ...

(continue 3–5 entries)
```

Use the Write tool — these are placeholder empty files from Task 1, so a full write is correct.

- [ ] **Step 4: Verify January is complete**

Run:
```bash
find "C:/Vibecoding/News/2026-01" -name "*.md" -size 0
```
Expected: empty output (no zero-byte files remain).

Spot-check 3 random files:
- Open them
- Confirm each has the `# <Subcategory> — January 2026` heading
- Confirm 3–5 entries (or 1–2 with a slim-month note)
- Confirm each entry has a link, Source, Date, and "Why this matters" line

- [ ] **Step 5: STOP — Pilot review checkpoint**

**Do not start February.** Report to the user:

> "January 2026 is curated and ready for review. Open `C:\Vibecoding\News\2026-01\` and sample a few files. Let me know if format, depth, or curation taste need adjustment before I parallelize Feb–May."

Wait for explicit approval before proceeding to Task 4.

---

## Reusable Methodology Block (referenced by Tasks 4–7)

Each month-curation task follows this identical methodology. It is reproduced inline at each task so a subagent dispatched on a single task has everything they need.

**The 16 files for a given month `YYYY-MM`:**

- `C:\Vibecoding\News\YYYY-MM\Technology\AI\Models.md`
- `C:\Vibecoding\News\YYYY-MM\Technology\AI\Research.md`
- `C:\Vibecoding\News\YYYY-MM\Technology\AI\Industry.md`
- `C:\Vibecoding\News\YYYY-MM\Technology\AI\Products-Agents.md`
- `C:\Vibecoding\News\YYYY-MM\Technology\AI\Policy-Safety.md`
- `C:\Vibecoding\News\YYYY-MM\Technology\Hardware-Chips.md`
- `C:\Vibecoding\News\YYYY-MM\Technology\Cybersecurity.md`
- `C:\Vibecoding\News\YYYY-MM\Politics\US.md`
- `C:\Vibecoding\News\YYYY-MM\Politics\International.md`
- `C:\Vibecoding\News\YYYY-MM\Science\Space.md`
- `C:\Vibecoding\News\YYYY-MM\Science\Health-Medicine.md`
- `C:\Vibecoding\News\YYYY-MM\Science\Climate.md`
- `C:\Vibecoding\News\YYYY-MM\Business-Economy\Markets-Macro.md`
- `C:\Vibecoding\News\YYYY-MM\Business-Economy\Crypto-Fintech.md`
- `C:\Vibecoding\News\YYYY-MM\World\Major-Events.md`
- `C:\Vibecoding\News\YYYY-MM\Culture\Notable.md`

**Search query patterns (substitute month name):**

| Subcategory | Example queries |
|---|---|
| Technology/AI/Models | "most significant AI model release <MONTH> 2026", "GPT Claude Gemini new model <MONTH> 2026" |
| Technology/AI/Research | "AI research breakthrough <MONTH> 2026", "machine learning paper <MONTH> 2026" |
| Technology/AI/Industry | "AI company funding acquisition <MONTH> 2026", "OpenAI Anthropic news <MONTH> 2026" |
| Technology/AI/Products-Agents | "AI agent product launch <MONTH> 2026", "enterprise AI deployment <MONTH> 2026" |
| Technology/AI/Policy-Safety | "AI regulation <MONTH> 2026", "AI safety policy <MONTH> 2026" |
| Technology/Hardware-Chips | "semiconductor chip announcement <MONTH> 2026", "Nvidia AMD Intel <MONTH> 2026" |
| Technology/Cybersecurity | "major cyberattack data breach <MONTH> 2026", "ransomware <MONTH> 2026" |
| Politics/US | "US politics major news <MONTH> 2026", "Congress White House <MONTH> 2026" |
| Politics/International | "international politics major news <MONTH> 2026", "election news <MONTH> 2026" |
| Science/Space | "space launch discovery <MONTH> 2026", "NASA SpaceX <MONTH> 2026" |
| Science/Health-Medicine | "medical breakthrough drug approval <MONTH> 2026", "FDA approval <MONTH> 2026" |
| Science/Climate | "climate change major news <MONTH> 2026", "climate policy <MONTH> 2026" |
| Business-Economy/Markets-Macro | "Federal Reserve markets <MONTH> 2026", "GDP inflation <MONTH> 2026" |
| Business-Economy/Crypto-Fintech | "Bitcoin crypto major news <MONTH> 2026", "fintech news <MONTH> 2026" |
| World/Major-Events | "biggest world news <MONTH> 2026", "global crisis <MONTH> 2026" |
| Culture/Notable | "major cultural event <MONTH> 2026", "notable death award <MONTH> 2026" |

**Curation rules:**
- 3–5 stories per subcategory.
- Authoritative outlets first (Reuters, AP, Bloomberg, FT, NYT, WSJ, Nature, Science, MIT Tech Review, Ars Technica, The Verge).
- Real-world impact, not hype. Multi-outlet coverage is a positive signal.
- Confirm date is in-month before including.
- If fewer than 3 strong stories: ship 1–2 with a top-of-file note `> Slim month — only N significant stories found.` Do not pad.

**Per-file template:**

```markdown
# <Subcategory> — <Month YYYY>

## 1. [Headline](https://source.url)
**Source:** Outlet · **Date:** YYYY-MM-DD

Why this matters: One or two sentences on real-world significance.

## 2. [Headline](https://source.url)
**Source:** Outlet · **Date:** YYYY-MM-DD

Why this matters: ...

(continue 3–5 entries)
```

**Write tool note:** The placeholder files from Task 1 are empty, so a full Write is correct for each file.

---

## Task 4: Curate February 2026

**Files:** 16 files under `C:\Vibecoding\News\2026-02\` (full list in Reusable Methodology Block above).

- [ ] **Step 1: Research February 2026 news per subcategory**

Apply the Reusable Methodology Block above with `<MONTH>` = "February" and `YYYY-MM` = `2026-02`. Run WebSearch for each subcategory, WebFetch when a date or claim needs verification.

- [ ] **Step 2: Curate 3–5 stories per subcategory**

Apply the curation rules from the Methodology Block. Slim-month note if under 3 strong stories.

- [ ] **Step 3: Write each of the 16 subcategory files**

Use the Write tool with the per-file template, substituting "February 2026" in the heading and `2026-02-DD` in entry dates.

- [ ] **Step 4: Verify**

```bash
find "C:/Vibecoding/News/2026-02" -name "*.md" -size 0
```
Expected: empty output (no zero-byte files remain).

Spot-check 3 random files — heading present, 3–5 entries (or slim-month note), every entry has link/Source/Date/Why this matters.

---

## Task 5: Curate March 2026

**Files:** 16 files under `C:\Vibecoding\News\2026-03\` (full list in Reusable Methodology Block above).

- [ ] **Step 1: Research March 2026 news per subcategory**

Apply the Reusable Methodology Block above with `<MONTH>` = "March" and `YYYY-MM` = `2026-03`.

- [ ] **Step 2: Curate 3–5 stories per subcategory**

Apply the curation rules from the Methodology Block.

- [ ] **Step 3: Write each of the 16 subcategory files**

Heading: "March 2026". Entry dates: `2026-03-DD`.

- [ ] **Step 4: Verify**

```bash
find "C:/Vibecoding/News/2026-03" -name "*.md" -size 0
```
Expected: empty output.

Spot-check 3 random files.

---

## Task 6: Curate April 2026

**Files:** 16 files under `C:\Vibecoding\News\2026-04\` (full list in Reusable Methodology Block above).

- [ ] **Step 1: Research April 2026 news per subcategory**

Apply the Reusable Methodology Block above with `<MONTH>` = "April" and `YYYY-MM` = `2026-04`.

- [ ] **Step 2: Curate 3–5 stories per subcategory**

Apply the curation rules from the Methodology Block.

- [ ] **Step 3: Write each of the 16 subcategory files**

Heading: "April 2026". Entry dates: `2026-04-DD`.

- [ ] **Step 4: Verify**

```bash
find "C:/Vibecoding/News/2026-04" -name "*.md" -size 0
```
Expected: empty output.

Spot-check 3 random files.

---

## Task 7: Curate May 2026 (partial — through 2026-05-26)

**Files:** 16 files under `C:\Vibecoding\News\2026-05\` (full list in Reusable Methodology Block above).

**Important:** Today is 2026-05-26. Include only stories dated **2026-05-01 through 2026-05-26**. Strictly reject any story dated 2026-05-27 or later. Some subcategories may legitimately be slim for a partial month — use the slim-month note.

- [ ] **Step 1: Research May 2026 news per subcategory**

Apply the Reusable Methodology Block above with `<MONTH>` = "May" and `YYYY-MM` = `2026-05`. After WebSearch, verify each candidate story's date — reject anything dated after 2026-05-26.

- [ ] **Step 2: Curate 3–5 stories per subcategory (1–2 acceptable with slim-month note)**

Apply the curation rules from the Methodology Block.

- [ ] **Step 3: Write each of the 16 subcategory files**

Heading: "May 2026". Entry dates: `2026-05-DD` where DD ≤ 26.

- [ ] **Step 4: Verify**

```bash
find "C:/Vibecoding/News/2026-05" -name "*.md" -size 0
```
Expected: empty output (slim files should contain the slim-month note, not be empty).

Spot-check 3 random files — and verify no entry has a date after 2026-05-26.

---

## Task 8: Final pass

- [ ] **Step 1: Confirm every file is non-empty and well-formed**

```bash
find "C:/Vibecoding/News" -path "*/2026-*/*" -name "*.md" -size 0
```
Expected: empty output across all 5 months.

- [ ] **Step 2: Spot-check formatting consistency**

Open one file from each month and verify:
- `# <Subcategory> — <Month YYYY>` heading
- Numbered entries
- Each entry: Headline link, Source · Date, "Why this matters" line

- [ ] **Step 3: Report completion to user**

> "Backfill complete: 5 months × 16 subcategory files. Browse from `C:\Vibecoding\News\`. To refresh for a future month, ask me to 'build the news digest for YYYY-MM' and I'll follow the README's convention."

---

## Parallelization Note

Tasks 4–7 (February through May) are **fully independent** — different months, different folders, different research scopes. After Task 3 is approved, they can be dispatched in parallel via subagents (one subagent per month), each given this plan as context and told to execute their respective task only.

Task 3 (January pilot) must complete and be approved first — it sets the bar for curation taste and format.
