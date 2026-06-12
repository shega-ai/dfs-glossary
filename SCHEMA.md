# Schema / Data Dictionary

Each record in `data/am.jsonl`, `data/om.jsonl` (and the matching `.csv` files)
is a single glossary entry with the following fields, in this order:

| Field | Type | Required | Description |
|-------|------|:--------:|-------------|
| `id` | string | ✓ | Stable, language-prefixed identifier (`am-001`, `om-001`). Zero-padded to 3 digits. **Never reused or renumbered.** |
| `term_en` | string | ✓ | The English term. **This is the join key** linking the same concept across languages. |
| `term_local` | string | ✓ | The term in the target language (Ge'ez script for `am`, Latin script for `om`). |
| `language` | string | ✓ | ISO 639-1 code: `am` (Amharic) or `om` (Afaan Oromoo). |
| `category` | string \| null | — | Domain grouping (e.g. `Channel`, `Concept`, `Process`, `Role/Actor`). Stored **verbatim** from the source; values are not yet normalised to a controlled vocabulary. `null` where the source provides no category. |
| `definition_local` | string | ✓ | The verified definition, in the target language. |
| `definition_en` | string \| null | — | The English definition, where available. |
| `example_local` | string \| null | — | A usage example, in the target language. `null` where the source provides none. |
| `example_en` | string \| null | — | The English usage example, where available. |
| `version` | string | ✓ | Dataset version this entry belongs to (`1.0`). |

## Notes

- **Encoding:** all files are UTF-8. Ge'ez text is stored exactly as in the
  verified source (no Unicode re-normalisation).
- **Cross-language join:** `am` and `om` records describing the same concept
  share the same `term_en` (compared case-insensitively, ignoring whitespace).
  Most entries match; a small number are written differently in the two source
  documents (e.g. with or without a parenthetical acronym) and do not join
  automatically.
- **Cross-fill:** `category` is sourced from the Afaan Oromoo deck and copied
  onto matching Amharic entries; `definition_en` / `example_en` are sourced from
  the Amharic deck and copied onto matching Afaan Oromoo entries. Fields that
  could not be matched remain `null`.
- **Nullable fields** (`category`, `definition_en`, `example_local`,
  `example_en`) may be absent for some entries; consumers should not assume they
  are always present.
