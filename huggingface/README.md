---
license: cc-by-4.0
pretty_name: DFS Glossary — Amharic & Afaan Oromoo
language:
  - am
  - om
multilinguality:
  - multilingual
tags:
  - finance
  - digital-financial-services
  - dfs
  - glossary
  - terminology
  - ethiopia
  - low-resource
size_categories:
  - n<1K
task_categories:
  - translation
  - text-classification
configs:
  - config_name: am
    data_files: am.jsonl
  - config_name: om
    data_files: om.jsonl
---

# DFS Glossary — Amharic & Afaan Oromoo

Expert-verified glossaries of **Digital Financial Services (DFS)** terminology in
**Amharic (`am`)** and **Afaan Oromoo (`om`)**, published as structured,
machine-readable, openly-licensed data.

Open language infrastructure for two low-resource Ethiopian languages — for
developers, researchers, translators, and the financial-inclusion community.

| | |
|---|---|
| Languages | Amharic (`am`, Ge'ez script) · Afaan Oromoo (`om`, Latin script) |
| Entries | 87 Amharic + 86 Afaan Oromoo = **173** |
| License | CC BY 4.0 |
| Version | 1.0 |

## Usage

```python
from datasets import load_dataset

am = load_dataset("shega/dfs-glossary", "am")   # Amharic glossary
om = load_dataset("shega/dfs-glossary", "om")   # Afaan Oromoo glossary

print(am["train"][0]["term_local"])  # should print clean Ge'ez, e.g. የአገልግሎት ነጥብ
```

## Data fields

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Stable, language-prefixed id (`am-001`, `om-001`). Never reused. |
| `term_en` | string | English term — the join key across languages. |
| `term_local` | string | Term in the target language (Ge'ez / Latin). |
| `language` | string | `am` or `om`. |
| `category` | string \| null | Domain grouping (e.g. `Channel`, `Concept`, `Process`). Verbatim from source. |
| `definition_local` | string | Verified definition in the target language. |
| `definition_en` | string \| null | English definition, where available. |
| `example_local` | string \| null | Usage example in the target language. |
| `example_en` | string \| null | English usage example, where available. |
| `version` | string | Dataset version (`1.0`). |

The English term (`term_en`) is shared across the two languages, so the `am` and
`om` configs can be joined on it.

## Methodology

Translated and verified by domain experts as part of the AKOFADA project, and
built under a strict fidelity policy:

- **Source is the editable copy decks, never the PDFs.** Ge'ez (Amharic) script
  corrupts when copied out of PDFs; for a terminology dataset a single wrong
  character destroys trust. PDFs are used only for human spot-checks.
- **Text is preserved verbatim** — only whitespace tidying is applied. No
  spelling, wording, casing, or Unicode normalisation of the verified text.
- **The two languages are cross-linked** on the English term.

## Provenance

- **Producer:** Shega
- **Project:** AKOFADA
- **Funding:** Gates Foundation

## Citation

<!-- TODO: replace with the Zenodo DOI once the GitHub v1.0 release is archived. -->

```bibtex
@dataset{shega_dfs_glossary_2026,
  title  = {DFS Glossary — Amharic & Afaan Oromoo},
  author = {Shega and AKOFADA},
  year   = {2026},
  version = {1.0},
  publisher = {Shega},
  note   = {DOI pending — to be added on first release},
  url    = {https://huggingface.co/datasets/shega/dfs-glossary}
}
```

## License

[Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).
Free to share and adapt, including commercially, with attribution.
