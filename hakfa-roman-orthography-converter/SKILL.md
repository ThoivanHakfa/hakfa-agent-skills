---
name: hakfa-roman-orthography-converter
description: Expertise in converting Hakfa Roman Orthography across five systems — FHL IME (PFS-style 1–6 numeric), FHL dict (POJ-style 1–8 numeric), 長老教會 PFS (1–6 numeric + Unicode diacritics), KPPY / 教育部客家語拼音方案 (numeric + modifier-letter diacritics), and IPA (with Chao tone letters). Handles all Input ↔ Unicode and cross-system conversions, including PFS ↔ KPPY orthographic mapping.
---

# Hakfa Roman Orthography Converter

## Guidelines

- **Orthography**: Use the term **Roman Orthography** (not "Romanization"). Prefer **Hakfa Latin-script Orthography** or **Hakfa Roman-script Orthography**.
- **Naming**: Refer to the language as **Hakfa** (or **Hak-fa**). Avoid "Hakka Chinese", "Taiwanese Hakka", or treating Hakfa as a dialect of Mandarin/Chinese.
- **Default dialect**: **Si-yen (四縣)** unless otherwise specified.

## Systems In Scope

This skill covers five systems (FHL IME, FHL dict, PFS, KPPY, IPA) and seven canonical machine formats.

| System | Description | Numeric format | Unicode / glyph format |
|:-------|:------------|:---------------|:-----------------------|
| **FHL IME** | The 信望愛 Hakfa Input Method (信望愛客語輸入法). Uses PFS orthography with **PFS-style 1–6 tone numbering** — input format is identical to PFS_INPUT. | **PFS_INPUT** | **PFS_UNICODE** |
| **FHL dict** | The numeric format used by the [信望愛 Hak-fa FHL Dictionary](https://hakka.fhl.net/dict/index_hakka.html). Diacritics are PFS, but **tone numbers borrow POJ 1–8 numbering** (number ↔ diacritic mapping shared with Taigi POJ). | **FHL_DICT_INPUT** | **FHL_UNICODE** (= PFS_UNICODE as a string) |
| **PFS** | **Pha̍k-fa-sṳ**, the 長老教會 (Presbyterian) tradition. Six tone slots with traditional numbering **1–6** (canonical examples: sî, sì, sí, si, se̍k, sek). The script of the FHL Hak-fa Dictionary and most historical Presbyterian Hak-fa publications. | **PFS_INPUT** (uses `ii` for `ṳ`) | **PFS_UNICODE** (uses `ṳ`) |
| **KPPY** | **Kàu-pō͘ Phin-yîm** (教育部客家語拼音方案), also called MOE standard. Different consonant inventory from PFS; uses modifier-letter tone marks (ˊ ˇ ˋ) placed after the syllable. The MOE dictionary displays tones in three modes: **調號** (八聲 slot: 1,2,3,4,5,8), **調型** (diacritic marks / 符號式), **調值** (Chao pitch / 數字式: ²⁴,¹¹,³¹,⁵⁵,⁵,²). The KonvertToPFS reference library departs from MOE 八聲 調號 by aligning its `KPPY_INPUT` digits 1–6 with PFS slots; only 調型 round-trips through `KPPY_UNICODE`. | **KPPY_INPUT** (trailing 1–6 ASCII digit, PFS-aligned per the KonvertToPFS library — e.g. `hag5-ga1-fa4`; **NOT** MOE 八聲 調號 and **NOT** 調值 superscripts) | **KPPY_UNICODE** (modifier-letter tone marks / 調型) |
| **IPA** | International Phonetic Alphabet, with **Chao tone letters** for tone (e.g. ˨˦, ˥˥). Used by the FHL data mirror's `Hakfa_IPA` column. **Single-syllable citation form only** — see scope note below. | — | **IPA** |

> **Critical**: FHL dict-numeric, PFS-numeric, and KPPY-numeric look superficially similar but use **incompatible numbering schemes**. FHL dict uses POJ-style digit→diacritic mapping (1–8); PFS (and FHL IME) uses sequential 1–6; KPPY uses 八聲 調號 (1–8) and Chao 調值. All three use small integers — never transcode between them by digit value alone. Always pivot via the canonical PFS tone slot.

## The Master Tone Table (Si-yen)

All conversions pivot on the **PFS tone number** (1–6) and its canonical example word. Use this table as the source of truth.

| PFS # | PFS | FHL IME | FHL dict | KPPY 調號 | KPPY 調型 | KPPY 調值 | IPA | Coda |
|:-----:|:----|:--------|:---------|:---------:|:---------:|:---------:|:----|:-----|
| **1** | sî (◌̂) | si1 | si5 | **1** (陰平) | siˊ | si²⁴ | si˨˦ | open / nasal |
| **2** | sì (◌̀) | si2 | si3 | **5** (陽平) | siˇ | si¹¹ | si˩˩ | open / nasal |
| **3** | sí (◌́) | si3 | si2 | **2** (上聲) | siˋ | si³¹ | si˧˩ | open / nasal |
| **4** | si (unmarked) | si4 | si1 | **3** (去聲) | si | si⁵⁵ | si˥˥ | open / nasal |
| **5** | se̍k (◌̍) | sek5 | sek8 | **8** (陽入) | seg | seg⁵ | sek̚˥ | -p/-t/-k / -b/-d/-g |
| **6** | sek (unmarked) | sek6 | sek4 | **4** (陰入) | segˋ | seg² | sek̚˨ | -p/-t/-k / -b/-d/-g |

> **KPPY 調號 is 八聲 numbering** — it follows the traditional 陰平–陽入 progression (1, 2, 3, 4, 5, 8 in Si-yen), NOT a sequential 1–6 scheme. Only 調號 1 aligns with PFS # 1; the rest diverge. Source: [哈客網路學院 聲調介紹](https://happyhakka.moe.edu.tw/Advanced/tone_2a.html).

> **KPPY tone marks**: KPPY uses **modifier letters placed after the syllable** (not combining diacritics on vowels). The modifier letters are: ˊ (U+02CA), ˇ (U+02C7), ˋ (U+02CB). KPPY also accepts Latin-diacritic equivalents (e.g. `gà` for `gaˋ`) as tolerant input.

> **IPA tone letters**: Use Unicode tone-letter blocks (U+02E5 ˥ extra-high … U+02E9 ˩ extra-low), composed left-to-right per Chao convention. Place tone letters at the end of the syllable, after segments. Some publications use Chao digits (e.g. `siˉ` written `si24`); prefer tone letters for the canonical IPA form.

## Numbering Systems Compared

| PFS # | PFS | FHL IME | FHL dict | KPPY 調號 | KPPY 調型 | KPPY 調值 | IPA |
|:-----:|:----|:--------|:---------|:---------:|:---------:|:---------:|:----|
| 1     | sî  | si1     | si5      | 1 (陰平)  | siˊ     | si²⁴    | si˨˦ |
| 2     | sì  | si2     | si3      | 5 (陽平)  | siˇ     | si¹¹    | si˩˩ |
| 3     | sí  | si3     | si2      | 2 (上聲)  | siˋ     | si³¹    | si˧˩ |
| 4     | si  | si4     | si1      | 3 (去聲)  | si        | si⁵⁵    | si˥˥ |
| 5     | se̍k | sek5    | sek8     | 8 (陽入)  | seg       | seg⁵     | sek̚˥ |
| 6     | sek | sek6    | sek4     | 4 (陰入)  | segˋ     | seg²     | sek̚˨ |

> **Four numbering systems, all using small integers, three incompatible.** FHL IME = PFS (no renumbering). FHL dict maps digits to POJ diacritics (FHL dict 1 = unmarked = PFS 4 去聲). KPPY 調號 follows 八聲 categories (1=陰平, 2=上聲, …). Always pivot via PFS #. See `references/linguistic_rules.md` §1 for the comprehensive cross-reference.

## Core Capabilities

### 1. Format Conversion

Seven canonical formats:

- **PFS_INPUT**  ↔ **PFS_UNICODE**  (FHL IME input is identical to PFS_INPUT)
- **FHL_DICT_INPUT**  ↔ **FHL_UNICODE**  (FHL_UNICODE is identical in glyphs to PFS_UNICODE)
- **KPPY_INPUT**  ↔ **KPPY_UNICODE**
- **IPA**  (one-way derivation from any of the above; reverse-mapping IPA → PFS/KPPY is lossy because IPA does not encode every spelling distinction)

Cross-conversions between systems require both **renumbering / re-encoding tones** and (for PFS↔KPPY / →IPA) **orthographic / phonemic mapping**.

### 2. Normalization

- **Tone-mark Placement**: Move tone marks to the correct vowel per system rules.
- **Han-Lo Spacing**: Fix spacing and punctuation between Hanji and Roman Orthography.
- **Punctuation Width**: Half-width ↔ full-width based on context.
- **Special character normalization**: PFS `ṳ` = `u` + U+0324 (combining diaeresis **below**). Distinct from `ü` (U+00FC) and `ŭ` (U+0306 breve).

### 3. Validation

- Validate syllables against Si-yen phonotactics.
- Reject impossible tone/coda combinations: PFS 5/6 require a stop coda; non-checked syllables cannot carry PFS 5/6.
- For FHL dict data: reject non-PFS-valid numerics (e.g. POJ tone 7 — does not occur in Si-yen Hakfa). For FHL IME data: validate as PFS_INPUT (digits 1–6).

## PFS ↔ KPPY Orthographic Mapping (Si-yen)

Cross-system conversion is **not** letter-for-letter. Aspiration is shifted by one slot, and `ṳ` is spelled out.

| Feature                  | PFS                       | KPPY                        |
|:-------------------------|:--------------------------|:----------------------------|
| Voiceless unaspirated    | `p` `t` `k`               | `b` `d` `g`                 |
| Voiceless aspirated      | `ph` `th` `kh`            | `p` `t` `k`                 |
| Affricates (unaspirated) | `ts`                      | `z`                         |
| Affricates (aspirated)   | `tsh`                     | `c`                         |
| Sibilant                 | `s`                       | `s`                         |
| Voiced labio-dental      | `v`                       | `v`                         |
| Velar nasal              | `ng`                      | `ng`                        |
| Glottal                  | `h`                       | `h`                         |
| Close central vowel      | `ṳ` (u + U+0324) or `ii` (PFS_INPUT)          | `ii`                        |
| Rising u-onglide medial  | `oV` (`oa`, `oai`, `oan`, `oang`, `oat`, `oak`, `oe`, `oen`, `oet`) | `uV` (`ua`, `uai`, `uan`, `uang`, `uad`, `uag`, `ue`, `uen`, `ued`) |
| Final stops (PFS 5/6)     | `-p` `-t` `-k`            | `-b` `-d` `-g`              |
| Syllable boundary        | `-` (hyphen)              | ` ` (space)                 |

> **Pitfall**: PFS `pa` (unaspirated) → KPPY `ba`, and PFS `pha` (aspirated) → KPPY `pa`. A naïve letter-swap inverts the aspiration contrast.

> **Rising u-onglide**: PFS spells the medial `[u]` onglide as `oV` (瓜 kôa, 關 koân, 怪 koái, 國 koet); KPPY spells it `uV` (gua, guan, guai, gued). Only `oa-` / `oe-` shift — bare PFS `o-` is a different rhyme, and KPPY `oi` (愛 oi, /oi/) is also distinct from PFS `oi`. See `references/linguistic_rules.md` §4.

## PFS → IPA Mapping (Si-yen)

### Initials

| PFS  | IPA   |  | PFS         | IPA   |
|:-----|:------|:-|:------------|:------|
| p    | p     |  | ch (or ts)  | ts    |
| ph   | pʰ    |  | chh (or tsh)| tsʰ   |
| m    | m     |  | s           | s     |
| f    | f     |  | k           | k     |
| v    | ʋ     |  | kh          | kʰ    |
| t    | t     |  | ng          | ŋ     |
| th   | tʰ    |  | h           | h     |
| n    | n     |  | (∅)         | (no onset / zero-onset) |
| l    | l     |  |             |       |

> **PFS spelling variants**: Older missionary-era PFS sources (Basel Mission, MacIver 1905, 1924 Shantou NT) write the affricate series as `ts` / `tsh`; modern Taiwan PFS (including the FHL Hak-fa Dictionary and 2012 客語聖經) uses `ch` / `chh`. Treat them as equivalent at the phonemic level. Output PFS should always use `ch` / `chh`.

> **`v` → `ʋ`**: Si-yen `v` is canonically realised as a labio-dental approximant `ʋ`, not the fricative `v`. Some sources transcribe it as `v` for typographic convenience — pick one and document it.

### Palatalization Before `/i/`

In Si-yen, the alveolar series palatalises to alveolo-palatal before `/i/`. Apply these rules **before** the general initial mapping above:

| PFS onset + i  | IPA          |
|:---------------|:-------------|
| ch(i)  / ts(i) | tɕi          |
| chh(i) / tsh(i)| tɕʰi         |
| s(i)           | ɕi           |
| ng(i)          | ɲi           |

Without this step, alveolar-onset syllables before `/i/` produce phonetically wrong IPA.

### Vowels

| PFS  | IPA   | Notes |
|:-----|:------|:------|
| a    | a     |       |
| e    | e     |       |
| i    | i     |       |
| o    | o     |       |
| u    | u     |       |
| ṳ    | ɨ     | close central unrounded; some sources prefer `ɿ` (apical) — pick one and note in project README |
| er   | ɤ     | mid-back unrounded; appears in a small number of Si-yen forms |

### Finals (codas)

| PFS  | IPA   | Notes |
|:-----|:------|:------|
| -m   | m     |       |
| -n   | n     |       |
| -ng  | ŋ     |       |
| -p   | p̚    | unreleased; some sources omit the no-release diacritic |
| -t   | t̚    | unreleased |
| -k   | k̚    | unreleased |

### Syllabic nasals

| PFS  | IPA   |
|:-----|:------|
| m    | m̩    |
| n    | n̩    |
| ng   | ŋ̍    |

### Tone

Append the Chao tone letters from the Master Tone Table to the segmental IPA:

- PFS 1 (sî) → `si˨˦` — 陰平 (KPPY 調值 ²⁴)
- PFS 5 (se̍k) → `sek̚˥` — 陽入 (KPPY 調值 ⁵)
- PFS 6 (sek) → `sek̚˨` — 陰入 (KPPY 調值 ²)

For checked tones (PFS 5/6), the tone letter is short (single tone letter) — reflecting the brief duration of stop-final syllables.

### IPA Scope: Single-Syllable Citation Form Only

**This skill produces IPA only at the single-syllable / citation-tone level. Tone sandhi is NOT applied.**

Each syllable receives the citation tone from the Master Tone Table — the pitch it would carry when spoken in isolation. Hak-fa Si-yen has well-known sandhi patterns (e.g. PFS 2 ˩˩ → ˧˥ before certain following tones; PFS 5 / PFS 6 sandhi in compounds), but those depend on the prosodic context of surrounding syllables and are out of scope here.

When converting multi-syllable input:

- Convert each syllable independently using its citation tone.
- Concatenate with the project's chosen syllable separator (hyphen, space, or no separator).
- Do **not** modify any tone letter based on neighbouring syllables.

If tone sandhi is required for a downstream application (e.g. speech synthesis, prosodic analysis), apply it as a separate post-processing step outside this skill.

## Tone-Mark Placement (PFS Unicode)

Hak-fa PFS adopts the **canonical POJ Section 21 placement rule letter-for-letter** — empirically confirmed across ~30,420 marked syllables in the FHL dictionary corpus. The diacritic lands by *letter position*, not by a "syllabic nucleus" priority.

1. **Single vowel** → mark that vowel.
2. **No vowel** → mark the nasal (`m`, `n`, `ng` — treat `ng` as 1 unit).
3. **Compound vowels** → mark the **2nd letter from the right** (treating `ng` as 1 unit).
   - **Exception 1**: If 2nd-from-right is `i` → mark **rightmost** instead (`liù`, `siá`).
   - **Exception 2**: **Checked** syllable + 2nd-from-right is `i`/`u` (but not `iu`/`iu`+stop) → mark **3rd letter**.
   - **Special**: `iu`+stop → 2nd-from-right (no exception fires; e.g. `liu̍k`).
4. **`ṳ` as nucleus** → diacritic combines on the `u`; the trema-below (U+0324) and the tone diacritic stack via NFC (U+0324 first, then tone-combining like U+0302 / U+0300 / U+0301 / U+030D), e.g. `sṳ̂`.
5. **Syllabic nasal `m`** (e.g. negative 唔 → `m̀`) → mark on the `m`. Syllabic `ng` → combining attaches to `n` (the leading codepoint of the 1-unit `ng`); `n` alone is rare in Si-yen.

> **Common pitfall**: `iu` → mark `u` (`liù`, `niù`), **not** `i`. The older "nucleus" heuristic that places it on `i` contradicts the FHL corpus and POJ Section 21.

> **Worked examples**: `khúa`, `koái`, `kuái`, `khoán`, `koe̍t`, `liâng`, `siông`, `siá`, `liù`, `kúi`, `liu̍k`, `sṳ̂`, `ǹg`, `m̀`. Full table with rule-fired column in `references/linguistic_rules.md` §2.

> KPPY placement rules differ in detail — especially around `ii`, palatalized initials, and word-final glides. Document per-publication when converting at scale.

## Conversion Pipeline

1. **NFC-normalize** the input.
2. **Segment** syllables on `-` (hyphen) for PFS/FHL systems, or on spaces for KPPY. Preserve inter-word spacing.
3. **Decode tone**: extract trailing digit (Input) or combining diacritic (Unicode) and map to the canonical PFS tone slot (1–6).
4. **Orthographic / phonemic map**: for PFS↔KPPY swap initials/finals/`ṳ`. For tone: map PFS # → KPPY 調號 / 調型 / 調值 via the master tone table (the three numbering systems are incompatible — see §Numbering Systems Compared). For →IPA, apply the PFS→IPA tables above (or convert to PFS first if starting from KPPY).
5. **Re-encode tone**: in target system's number, diacritic, or Chao tone letters, placed per target system's rules.
6. **Re-assemble** with hyphens for PFS/FHL output, spaces for KPPY output, or per project convention for IPA (many publications use spaces or zero-width separators between syllables).
7. **NFC-normalize** the output.

## Reference Library — KonvertToPFS

This skill's seven canonical formats align 1:1 with the [KonvertToPFS](https://github.com/Phakfasu/KonvertToPFS) Kotlin Multiplatform library (GPL-3.0-or-later). When you need a programmatic implementation, that library is the authoritative source.

- **Entry point**: `org.phakfasu.konverttopfs.KonvertToPfs.convert(text, from, to) → String`
- **`LomajiFormat` enum**: `PFS_INPUT`, `PFS_UNICODE`, `KPPY_INPUT`, `KPPY_UNICODE`, `FHL_DICT_INPUT`, `FHL_UNICODE`, `IPA` — the same seven formats this skill enumerates above.
- **Non-destructive**: mixed input (Hanji, punctuation, whitespace, non-syllabic tokens) is preserved verbatim. A token that fails Si-yen phonotactic validation is also emitted unchanged rather than mangled.
- **Casing preservation**: per-token casing (lower / Title / ALL-CAPS) is detected and reapplied on output.
- **Library deviation from MOE**: KPPY input digits are 1–6 (PFS-aligned), **not** MOE 八聲 調號. See pitfall #6 and `references/linguistic_rules.md` §1 / §11.

Full API surface, internal data model (`HakfaSyllable`), file map, and behavioral notes are in `references/linguistic_rules.md` §11.

## Usage Patterns

- "Convert FHL IME `ngai3` to PFS Unicode." → FHL IME uses PFS numbering, so `ngai3` = PFS 3 → `ngái`
- "Convert FHL dict `hak4-fa3-sṳ1` to PFS Unicode." → slot-decode (FHL dict 4→PFS 6, FHL dict 3→PFS 2, FHL dict 1→PFS 4) → `hak-fà-sṳ` (the entering tone diacritic shape is preserved across FHL↔PFS — FHL dict 4 unmarked-stop ↔ PFS 6 unmarked-stop; FHL dict 8 vline-stop ↔ PFS 5 vline-stop)
- "Convert FHL dict numeric `ngai2` to PFS numeric." → FHL dict 2 = PFS 3 → PFS `ngai3`
- "Convert PFS `Pha̍k-fa-sṳ` to KPPY." → `pag fa sii` (KPPY_UNICODE; PFS 5 → unmarked + stop with `-k` → `-g`; PFS 4 → unmarked; `ṳ` → `ii`; KPPY uses spaces, not hyphens)
- "Convert KPPY `hag5` (library `KPPY_INPUT`) to PFS Unicode." → `hag5` = library T5 = PFS 5 = 陽入 high-pitched checked → `ha̍k`. Note: in MOE 八聲 調號 the same syllable would be written `hag8` (調號 8 = 陽入); the KonvertToPFS library does **not** accept the MOE 號 form on input. See §1 of `references/linguistic_rules.md`.
- "Convert PFS `Pha̍k-fa-sṳ` to IPA." → `pʰak̚˥ fa˥˥ sɨ˥˥` (PFS 5 → ˥ (high-pitched checked); PFS 4 → ˥˥; citation tone per syllable, no sandhi; spacing/hyphens per project style)
- "Renumber a CSV column from FHL dict-numeric to PFS-numeric." → apply the master tone table row-by-row; never swap digits directly.
- "Validate whether FHL dict `set8` is a well-formed Si-yen syllable." → Yes (FHL dict 8 = PFS 5, vline-stop, requires stop coda — `-t` satisfies).

## FHL Dictionary Data Notes

When ingesting data from the [台語信望愛客語辭典 (Hak-fa FHL Dictionary)](https://hakka.fhl.net/dict/index_hakka.html) or its [data mirror](https://github.com/ThoivanHakfa/HakkaFHLDictDataMirror):

- **Digit conversion** (POJ-style → PFS 1–6): marked `{5→1, 3→2, 2→3, 8→5}`; unmarked → 4 (open/nasal coda) or 6 (stop coda).
- **Tone-mark placement diverges from canonical POJ on 52 syllables across the corpus.** FHL empirically marks the *first vowel of the cluster* (skipping a leading medial `i`); canonical POJ marks the 2nd letter from the right. Divergence cells: `oai` (16), `uai` (1), `oa`+coda (31), `oe`+coda (2), `ua`+coda (2). All other clusters already match.
- **`ṳ` trema-below restoration**: FHL drops U+0324 from `ṳ` when adding a tone diacritic (e.g. `sii5` → `sû` rather than `sṳ̂`). Restore U+0324 by aligning each toned `u` against numeric `ii`.
- **Per-row form detection is unsafe** (~12% ambiguity between FHL and PFS shape). Use a corpus-level detector before bulk re-conversion.
- The mirror's `bunji/HakfaFHLDict.csv` provides pre-normalised `PFS_Numeric` + canonical-placement `PFS_Unicode` + `Hakfa_IPA` — prefer it over re-scraping FHL.

Full algorithm, divergence tables, and reference Python (`_reposition_syllable`, `fhl_unicode_to_pfs_unicode`, `is_pfs_numeric_corpus`) in `references/linguistic_rules.md` §9.

## Resources

### references/
- `linguistic_rules.md`: Detailed tone-placement rules (§2), full PFS↔KPPY mapping tables (§4), IPA conventions (§5), validation (§7), **FHL Dictionary specifics + divergence cells (§9)**, the **comprehensive MOE-sourced initial / final inventory tables for Si-yen and Nam-Si-yen (§10)** including KPPY ↔ PFS ↔ IPA cross-reference, allophonic j/q/x, and the two finals (`ian` / `iad`) that distinguish the two sub-dialects, and **§11 KonvertToPFS Library API & File Map** (public API, `LomajiFormat` enum, `HakfaSyllable` model, per-file responsibilities). **MUST** read before bulk or cross-system conversions, before ingesting FHL data, or when validating syllables against the full Si-yen / Nam-Si-yen inventory.

## Common Pitfalls

1. **Confusing FHL dict with FHL IME**: The FHL dictionary uses POJ-style 1–8 numbering, but the FHL IME (信望愛客語輸入法) uses PFS-style 1–6 numbering. Always confirm which FHL source is in play — dict data needs renumbering via the master tone table; IME data can be treated as PFS_INPUT directly.
2. **Silent FHL dict ↔ PFS renumbering**: Both use small integers but with **incompatible** number→slot mappings. FHL dict 5 = circumflex (= PFS 1, sî); PFS 5 = vertical line + stop (se̍k, high-pitched checked). Always pivot via the canonical PFS slot — never swap numbers directly. The diacritic *shape* matches POJ between FHL dict and PFS for the checked tones (FHL dict 4 unmarked ↔ PFS 6 unmarked, low-pitched checked; FHL dict 8 vertical line ↔ PFS 5 vertical line, high-pitched checked).
3. **Borrowing POJ semantics for general Hakfa data**: FHL dict's POJ-style numbering is an FHL-dictionary convention only. Other Hakfa data sources (including the FHL IME) almost always use 長老教會 PFS 1–6 — confirm the source's convention before parsing.
4. **`ṳ` encoding**: PFS `ṳ` = `u` + U+0324 (diaeresis **below**). Distinct from `ü` (U+00FC, diaeresis above) and `ŭ` (U+0306 breve).
5. **PFS↔KPPY aspiration shift**: Letter-for-letter mapping silently inverts aspirated/unaspirated. Always apply the consonant table.
6. **KPPY numbering ambiguity**: KPPY tone digits come in **four** distinct conventions, all using small integers:
   - **MOE 調號 (八聲)**: 1,2,3,4,5,8 — the official 教育部 / 哈客網路學院 tone-category slot.
   - **MOE 調型 (符號式)**: ˊ ˇ ˋ modifier letters appended after the syllable (diacritic, not a digit).
   - **MOE 調值 (數字式)**: Chao pitch contour ²⁴,¹¹,³¹,⁵⁵,⁵,² appended as superscript to each syllable.
   - **KonvertToPFS `KPPY_INPUT`**: 1–6 PFS-aligned digits (T1=PFS 1 陰平, T2=PFS 2 陽平, T3=PFS 3 上聲, T4=PFS 4 去聲, T5=PFS 5 陽入 high-pitched checked, T6=PFS 6 陰入 low-pitched checked). The library *deliberately* deviates from MOE 八聲 調號 — see `Kppy.kt` lines 24-29 and §1 of `references/linguistic_rules.md`.

   The single-digit checked-tone 調值 (⁵ and ²) are easily confused with 調號 / library-digit values. Always confirm which convention is in play before parsing.
7. **KPPY 調號 ≠ PFS #**: KPPY 調號 follows the 八聲 framework — only 調號 1 = PFS 1; the rest diverge (調號 2 = PFS 3, 調號 3 = PFS 4, 調號 4 = PFS 6, 調號 5 = PFS 2, 調號 8 = PFS 5). Never assume KPPY numbers map 1↔1 to PFS.
8. **IPA tone-letter encoding**: Use the U+02E5–U+02E9 tone-letter block. Do not substitute superscript digits or Latin numerals — these are not equivalent and will not render correctly with most IPA fonts.
9. **IPA → orthography is lossy**: IPA collapses spelling distinctions that PFS / KPPY preserve (e.g. dialect-specific orthographic choices). Reverse conversion from IPA should be flagged as approximate.
10. **IPA tone sandhi is out of scope**: Always emit citation-tone IPA per syllable. Do not attempt sandhi inference from PFS/KPPY input — sandhi depends on prosodic boundaries this skill does not analyse.
11. **Dialect**: Default to Si-yen. For Hai-liu / Tai-pu / Rau-ping / Zhao-an, the slot-to-pitch mapping (and sometimes the consonant inventory) differs — re-derive the master table before converting. **Nam-Si-yen** shares Si-yen's initial inventory and tone slots but introduces two extra finals (`ian` [ian] and `iad` [iat̚]) after velar (`g, k, ng`) or zero initials; Si-yen merges both into `ien` / `ied`. When folding Nam-Si-yen → Si-yen, apply this merger; see `references/linguistic_rules.md` §10.4.
12. **`iu` placement**: Hak-fa PFS marks the **rightmost** letter — `liù`, **not** `líu` (Exception 1 of POJ Section 21). The older "syllabic nucleus" framing places it on `i` and contradicts the FHL corpus. See `references/linguistic_rules.md` §2.
13. **FHL graph=2 placement divergence**: FHL's Unicode column places the diacritic on the *first vowel* of the cluster, which conflicts with canonical POJ on 52 syllables (`oai` / `uai` / `oa`+coda / `oe`+coda / `ua`+coda). When deriving canonical PFS from FHL data, reposition per §2; keep the original FHL placement in a separate "raw" column for traceability. See §9.3.
14. **FHL drops U+0324 under tone diacritics**: `sii5` arrives from FHL as `sû`, not `sṳ̂`. Restore the trema-below by aligning each toned `u` against numeric `ii`. See §9.4.
