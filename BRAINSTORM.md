# DFS Glossary Dataset — Project Brainstorm & Plan

**Project:** Convert Shega/AKOFADA's expert-verified Digital Financial Services (DFS)
glossaries (Amharic + Afaan Oromoo) from PDF into structured, machine-readable,
openly-licensed datasets, and publish them where developers and researchers look.

**Funder/context:** AKOFADA project, Gates Foundation funded.
**Strategic goal:** Position Shega as a builder of open language infrastructure for
low-resource languages — not just a media company.

---

## The one rule that governs everything

> **Do NOT extract text from the PDFs.** Ge'ez script (Amharic) corrupts on PDF copy —
> characters get swapped/mangled. For a terminology dataset, one wrong character destroys
> trust. **All text must come from the original copy decks** (editable source: Word/Google
> Docs/design files). The PDFs are only used for *spot-check fidelity verification*.

---

## Target schema (per entry)

```json
{
  "id": "am-001",
  "term_en": "Financial Inclusion",
  "term_local": "አካታች ፋይናንስ",
  "language": "am",
  "category": "...",
  "definition": "...",
  "example": "...",
  "version": "1.0"
}
```

- `id` — stable, language-prefixed (`am-001`, `om-001`). Never reused/renumbered.
- `term_en` — English term (the join key across languages).
- `term_local` — term in target language (Ge'ez / Latin script).
- `language` — ISO code: `am` (Amharic), `om` (Afaan Oromoo).
- `category` — domain grouping. **OPEN QUESTION: in copy decks or must be derived?**
- `definition` — verified definition in the local language.
- `example` — usage example. **OPEN QUESTION: present in copy decks?**
- `version` — dataset version the entry belongs to (`1.0`).

**Counts to validate:** 87 Amharic + 86 Afaan Oromoo = **173 total**.

---

## Deliverables / artifacts (the 4 + 1 publishing surfaces)

| # | Surface | What lives there | Purpose |
|---|---------|------------------|---------|
| 1 | **GitHub** `shega/dfs-glossary` | data, README, LICENSE, CITATION.cff, PDFs, scripts, Issues | canonical source, community corrections |
| 2 | **Zenodo** | archived release | permanent **DOI** → academic citability |
| 3 | **Hugging Face** `shega/dfs-glossary` | JSONL/CSV + dataset card + tags | ML discovery channel (`load_dataset`) |
| 4 | **DFS Hub** `digitalfinance.shega.co/data` | links to all 3 | Shega-owned anchor |
| 5 | **Announcement** (LinkedIn/Masakhane/EthioNLP) | — | **Anteneh's job, post-launch. Not ours.** |

---

## Execution order (with dependencies)

### Step 0 — Unblock (do FIRST, has lead time) 🚧 BLOCKING
- [ ] Request original **copy decks** for both glossaries from content/design team.
- [ ] Confirm ownership/access: `shega` GitHub org, Shega Hugging Face org, Zenodo
      account, edit rights to `digitalfinance.shega.co`.
- [ ] Confirm citation/attribution: author names, how AKOFADA + Gates Foundation are
      credited, documented permission to open-source under CC BY 4.0.

### Step 1 — Extract & structure
- [ ] Map copy-deck structure → schema. Flag missing fields (`category`, `example`).
- [ ] Write `scripts/convert.py` → outputs `am.jsonl`, `am.csv`, `om.jsonl`, `om.csv`.
      (Script, not hand-copy — repeatable for v1.1 corrections.)
- [ ] Validate: UTF-8, every JSONL line parses, counts (87/86), no dup IDs, no empty
      required fields.
- [ ] **Fidelity spot-check** vs PDFs by a native reader, 10–15 entries/language,
      character-by-character. (This is THE credibility step.)

### Step 2 — GitHub repo
- [ ] Create `shega/dfs-glossary` (private while assembling).
- [ ] Structure: `data/`, `pdfs/`, `scripts/`, `README.md`, `LICENSE`, `CITATION.cff`.
- [ ] README: what it is, methodology (expert verification), provenance (AKOFADA/Gates),
      schema docs, citation, how to propose corrections.
- [ ] `LICENSE` = CC BY 4.0 full text. `CITATION.cff` (renders "Cite this repository").
- [ ] Enable Issues + templates ("Propose a term", "Report a correction").
- [ ] Make public.

### Step 3 — Zenodo DOI (order matters!)
- [ ] Log into Zenodo via GitHub, enable integration toggle for the repo **before** release.
- [ ] Cut **v1.0** GitHub release → Zenodo auto-archives + mints DOI.
- [ ] Fill Zenodo metadata: title, authors, description, license, keywords, funding.
- [ ] Copy DOI badge back into README + CITATION.cff.

### Step 4 — Hugging Face mirror
- [ ] Create HF dataset repo under Shega org, upload JSONL/CSV.
- [ ] Dataset card: description, languages, schema, methodology, `license: cc-by-4.0`,
      citation w/ DOI, tags `am`, `om`, `finance`, `ethiopia`.
- [ ] Test `load_dataset("shega/dfs-glossary")` returns clean Ge'ez text.

### Step 5 — DFS Hub
- [ ] Create "Data" page on `digitalfinance.shega.co` linking GitHub + HF + Zenodo DOI.

### Step 6 — Verify acceptance criteria & hand off
- [ ] 173 entries valid + spot-checked ✓
- [ ] GitHub public w/ README/LICENSE/citation ✓
- [ ] HF live w/ complete card ✓
- [ ] DOI minted ✓
- [ ] DFS Hub "Data" page live ✓
- [ ] Hand the 3 links to Anteneh/comms for announcement.

**Practical critical path:** assemble repo → enable Zenodo → publish+release → get DOI →
update README → publish HF card with DOI.

---

## Open questions to resolve with the team

1. **Ownership** — who controls the `shega` GitHub org and HF namespace?
2. **Field coverage** — do copy decks contain `category` and `example`, or must they be
   derived/authored? (Affects whether Step 1 is mechanical or needs editorial input.)
3. **Authorship** — citation should name whom? Shega? the expert verifiers? AKOFADA?
4. **Cross-language linking** — should `am-001` and `om-001` share the same `term_en` so
   the two files can be joined? Worth aligning IDs by English term if possible.

---

## Risks

- **Biggest risk = Step 0–1**: getting clean copy decks + verifying character fidelity.
  Everything from Step 2 on is ~1–2 days of mechanical work once data is clean.
- If copy decks are themselves PDF-derived, we've gained nothing — must confirm provenance.
- Ge'ez normalization: decide on Unicode normalization form (NFC recommended) and apply
  consistently in the converter.
