# DFS Glossary — Amharic & Afaan Oromoo

Expert-verified glossaries of **Digital Financial Services (DFS)** terminology in
**Amharic (`am`)** and **Afaan Oromoo (`om`)**, published as structured,
machine-readable, openly-licensed datasets.

This is open language infrastructure for two low-resource Ethiopian languages —
intended for developers, researchers, translators, and the financial-inclusion
community.

| | |
|---|---|
| **Languages** | Amharic (`am`, Ge'ez script) · Afaan Oromoo (`om`, Latin script) |
| **Entries** | 87 Amharic + 86 Afaan Oromoo = **173** |
| **Format** | JSONL + CSV (UTF-8) |
| **License** | [CC BY 4.0](LICENSE) |
| **Version** | 1.0 |

## Data

| File | Description |
|------|-------------|
| [`data/am.jsonl`](data/am.jsonl) / [`data/am.csv`](data/am.csv) | Amharic glossary, one record per line |
| [`data/om.jsonl`](data/om.jsonl) / [`data/om.csv`](data/om.csv) | Afaan Oromoo glossary, one record per line |

Each record follows the schema documented in [`SCHEMA.md`](SCHEMA.md). The English
term (`term_en`) is the join key across the two languages.

```json
{
  "id": "am-001",
  "term_en": "Access Point",
  "term_local": "የአገልግሎት ነጥብ",
  "language": "am",
  "category": "Channel",
  "definition_local": "ተጠቃሚዎች፤ ክፍያዎችን፣ ገንዘብ መላክ/መቀበልን…",
  "definition_en": "A physical or digital location where users can interact with…",
  "example_local": "አንድ ግለሰብ በሞባይል-ዋሌቱ ውስጥ ያለውን ቀሪ ገንዘቡን…",
  "example_en": "A mobile money agent kiosk or a USSD code…",
  "version": "1.0"
}
```

## Methodology

These glossaries were **translated and verified by domain experts** as part of the
AKOFADA project. To preserve that verification, the datasets are built under a
strict fidelity policy:

- **Source is the editable copy decks** (Word documents), **never the PDFs.**
  Ge'ez (Amharic) script corrupts when copied out of PDFs — characters get
  swapped or mangled — and for a terminology dataset a single wrong character
  destroys trust. The PDFs are used only for human fidelity spot-checks.
- **Text is preserved verbatim.** The conversion script ([`scripts/convert.py`](scripts/convert.py))
  applies *only* whitespace tidying (trimming and collapsing spaces, normalising
  the non-breaking space). No spelling, wording, casing, or Unicode
  normalisation is applied to the verified term, definition, or example text.
- **The two languages are cross-linked** on the English term, which lets the
  Amharic and Afaan Oromoo files be joined.

## Reproducing the data

The datasets are generated from the source copy decks in [`docs/`](docs/):

```bash
pip install python-docx
python scripts/convert.py
```

This writes the four files under [`data/`](data/) and validates counts
(87 / 86), unique IDs, required fields, and UTF-8 round-tripping.

## Provenance

- **Producer:** Shega
- **Project:** AKOFADA
- **Funding:** Gates Foundation

## Citation

See [`CITATION.cff`](CITATION.cff) — GitHub renders a **"Cite this repository"**
button from it. (A Zenodo DOI will be added here on first release.)

## Contributing / corrections

Terminology evolves, and corrections are welcome. Please open an issue:

- **Propose a term** — suggest a new entry.
- **Report a correction** — flag an error in an existing entry.

Because the published text is expert-verified, substantive changes to a
definition or term are reviewed before being merged.

## License

This dataset is licensed under the
[Creative Commons Attribution 4.0 International License (CC BY 4.0)](LICENSE).
You are free to share and adapt it, including commercially, with attribution.
