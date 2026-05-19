# Hakfa Roman Orthography — Linguistic Rules

Detailed rules supporting the `hakfa-roman-orthography-converter` skill. Read this before any bulk conversion or cross-system mapping.

**Default dialect: Si-yen (四縣).** For other dialects (Hai-liu, Tai-pu, Rau-ping, Zhao-an), re-derive the tables before converting.

---

## 1. Tone Inventory & Numbering Crosswalk (Si-yen)

The single source of truth. All conversions pivot on the **PFS #** column (with its canonical example word).

| PFS # | PFS | FHL IME | FHL dict | KPPY 調號 | KPPY 調型 | KPPY 調值 | IPA | Coda |
|:-----:|:----|:--------|:---------|:---------:|:---------:|:---------:|:----|:-----|
| 1     | sî (◌̂)  | si1 | si5 | 1 (陰平) | siˊ | si²⁴ | si˨˦  | open / nasal |
| 2     | sì (◌̀)  | si2 | si3 | 5 (陽平) | siˇ | si¹¹ | si˩˩  | open / nasal |
| 3     | sí (◌́)  | si3 | si2 | 2 (上聲) | siˋ | si³¹ | si˧˩  | open / nasal |
| 4     | si (unmarked)  | si4 | si1 | 3 (去聲) | si   | si⁵⁵ | si˥˥  | open / nasal |
| 5     | se̍k (◌̍) | sek5 | sek8 | 8 (陽入) | seg   | seg⁵  | sek̚˥ | -p/-t/-k / -b/-d/-g |
| 6     | sek (unmarked) | sek6 | sek4 | 4 (陰入) | segˋ | seg²  | sek̚˨ | -p/-t/-k / -b/-d/-g |

### Why FHL dict ↔ PFS renumbering is a trap

| Number | FHL dict means | PFS means |
|:------:|:----------|:----------|
| 1 | unmarked (= PFS 4, si)              | circumflex (= PFS 1, sî) |
| 2 | acute (= PFS 3, sí)                 | grave (= PFS 2, sì) |
| 3 | grave (= PFS 2, sì)                 | acute (= PFS 3, sí) |
| 4 | unmarked + stop (= PFS 6, sek)      | unmarked (= PFS 4, si) |
| 5 | circumflex (= PFS 1, sî)            | vertical line + stop (= PFS 5, se̍k) |
| 6 | (unused in FHL)                      | unmarked + stop (= PFS 6, sek) |
| 8 | vertical line + stop (= PFS 5, se̍k) | (not used in PFS 1–6) |

A naïve `s/5/1/g` from FHL dict to PFS produces complete slot corruption. Note also that for entering tones, the diacritic *shape* is the same in both systems but the *number* differs: FHL dict 4 (unmarked + stop, e.g. `hak`) = PFS 6, and FHL dict 8 (vertical line + stop, e.g. `ha̍k`) = PFS 5.

> **FHL IME vs FHL dict**: The FHL IME (信望愛客語輸入法) uses PFS-style 1–6 numbering — identical to PFS_INPUT. Only the FHL dictionary website uses the POJ-style 1–8 numbering shown above. Always confirm which FHL source is in play before applying renumbering.

### Dictionary Tone Numbering — 八聲 Framework (Si-yen)

Both the FHL dict and KPPY (教育部) dictionaries use tone numbers from the eight-tone (八聲) slot set **{1, 2, 3, 4, 5, 8}** for Si-yen (tones 6 陽上 and 7 陽去 are merged). However, the two systems assign different meanings to the same numbers: KPPY 調號 follows the 八聲 categories directly (1 = 陰平, 2 = 上聲, 3 = 去聲, 4 = 陰入, 5 = 陽平, 8 = 陽入); FHL dict numbers select the POJ-equivalent diacritic shape (see the FHL dict ↔ PFS trap table above), so FHL dict 1 = 去聲 (not 陰平). The FHL IME, by contrast, uses PFS-style 1–6 numbering and does not require renumbering.

#### Comprehensive Cross-Reference (Si-yen / Nam-si-yen)

| 八聲 | 調類 (MOE) | PFS # | PFS | FHL IME | FHL dict | KPPY 調號 | KPPY 調型 | KPPY 調值 | IPA | Coda |
|:----:|:-----------|:-----:|:----|:--------|:---------|:---------:|:---------:|:---------:|:----|:-----|
| 1 | 陰平 | 1 | sî (◌̂) | si1 | si5 | 1 | siˊ | si²⁴ | si˨˦ | open / nasal |
| 2 | 上聲 | 3 | sí (◌́) | si3 | si2 | 2 | siˋ | si³¹ | si˧˩ | open / nasal |
| 3 | 去聲 | 4 | si (unmarked) | si4 | si1 | 3 | si | si⁵⁵ | si˥˥ | open / nasal |
| 4 | 陰入 | 6 | sek (unmarked) | sek6 | sek4 | 4 | segˋ | seg² | sek̚˨ | -p/-t/-k / -b/-d/-g |
| 5 | 陽平 | 2 | sì (◌̀) | si2 | si3 | 5 | siˇ | si¹¹ | si˩˩ | open / nasal |
| 6 | — | — | — | — | — | — | — | — | — | merged in Si-yen (陽上) |
| 7 | — | — | — | — | — | — | — | — | — | merged in Si-yen (陽去) |
| 8 | 陽入 | 5 | se̍k (◌̍) | sek5 | sek8 | 8 | seg | seg⁵ | sek̚˥ | -p/-t/-k / -b/-d/-g |

> **FHL IME # = PFS #** — no renumbering needed. **FHL dict numbers track POJ diacritics** — FHL dict 1 = unmarked = PFS 4 (去聲). **KPPY 調號 tracks 八聲 categories** — 調號 1 = 陰平, 2 = 上聲, etc. The three 1–8 systems (FHL dict, KPPY 調號, 八聲) are **not** interchangeable — always pivot via PFS #. Source: [哈客網路學院 聲調介紹](https://happyhakka.moe.edu.tw/Advanced/tone_2a.html).

#### MOE 調號 vs KonvertToPFS KPPY digit

The MOE 八聲 調號 column above (1, 2, 3, 4, 5, 8) is the **linguistic standard** as documented by 教育部 and 哈客網路學院. The [KonvertToPFS](https://github.com/Phakfasu/KonvertToPFS) reference library, however, uses a **PFS-aligned 1–6 digit** for its `KPPY_INPUT` format — its T1…T6 map 1↔1 to PFS 1…6. This makes the library's KPPY digit a **fourth distinct numeric convention** in the Hak-fa landscape (alongside FHL dict POJ-style, KPPY 八聲 調號, and KPPY 調值 Chao pitch).

| Slot           | MOE 調號 | KonvertToPFS KPPY digit | KPPY 調型 (marker on canonical syllable) |
|:---------------|:--------:|:-----------------------:|:----------------------------------------|
| 陰平 (PFS 1)   | 1        | 1                       | `siˊ`                                   |
| 陽平 (PFS 2)   | 5        | 2                       | `siˇ`                                   |
| 上聲 (PFS 3)   | 2        | 3                       | `siˋ`                                   |
| 去聲 (PFS 4)   | 3        | 4                       | `si`                                    |
| 陽入 (PFS 5)   | 8        | 5                       | `seg` (unmarked on stop)                |
| 陰入 (PFS 6)   | 4        | 6                       | `segˋ` (grave on stop)                  |

The library's choice is deliberate — see `Kppy.kt` lines 24–29 ("This library aligns KPPY digit numbering with PFS … the official 教育部 KPPY 號 reverses these two slots; this library does not follow that convention"), and `SiyenTones.kt:byKppyNumber` which exposes the library-digit lookup as a separate map so callers ingesting raw 教育部 data can wire up an alternative table.

**Practical rules**:

- When transcoding **library-flavored** `KPPY_INPUT` (the format documented in this skill's "Systems In Scope" table), treat the trailing 1–6 digit as a PFS slot index.
- When ingesting **raw MOE 調號** data (1,2,3,4,5,8), renumber `{1→1, 2→3, 3→4, 4→6, 5→2, 8→5}` to PFS slots before any downstream conversion.
- The 調型 (符號式) column round-trips cleanly through `KPPY_UNICODE` and is unaffected by this divergence.

#### KPPY Three Display Modes (調號 / 調型 / 調值)

The official MOE dictionary (《臺灣客語辭典》) categorizes each tone using three KPPY display modes combined as `(調號/調型/調值)`. For example: `陰平(1/ˊ/24)` or `陰入(4/ˋ/2)`.

1. **KPPY 調號 (Tone Number)**: The 八聲 slot number (see 八聲 column above).
2. **KPPY 調型 (Tone Shape / 符號式)**: The modifier-letter diacritic mark placed after the syllable.
3. **KPPY 調值 (Tone Pitch Value / 數字式)**: The Chao pitch contour appended as superscript digits (e.g. si²⁴, si³¹, si⁵⁵).

For checked tones, the 調型 markers are: **陰入 (調號 4) = ˋ** on stop syllable; **陽入 (調號 8) = unmarked** on stop syllable. The stop coda (-b/-d/-g) itself signals an entering tone.

#### Tone-1 變調 Surface Form

| KPPY 調值 | KPPY marker | IPA | Notes |
|:---------:|:-----------:|:---:|:------|
| ³³ | `+` | ˧ | 陰平 (八聲 1, PFS 1) sandhi surface form — not an independent tone slot |

This sandhi form appears in the MOE dictionary's `詞目索引` annotations but does not occupy its own PFS or 八聲 slot. See §6 (Tone Sandhi: Out of Scope) for handling in this skill.

---

## 2. PFS Tone-Mark Placement Rules

For PFS Unicode output, place the tone diacritic on a single character per syllable. **Hak-fa PFS adopts the canonical POJ Section 21 placement rule letter-for-letter** — the diacritic lands by *letter position* (2nd from the right of the syllable, with `i`-exceptions), **not** by a "syllabic nucleus" priority. This is empirically confirmed by the ~30,420 marked syllables in the FHL dictionary corpus (see [HakkaFHLDictDataMirror](https://github.com/ThoivanHakfa/HakkaFHLDictDataMirror) and the Taigi reference at [Taigibun/taigibun-agent-skills · linguistic_rules.md](https://github.com/Taigibun/taigibun-agent-skills/blob/main/taigi-roman-orthography-converter/references/linguistic_rules.md)).

### Rule (canonical POJ Section 21, applied to Hak-fa)

1. **Single vowel** → mark that vowel.
2. **No vowel** → mark the nasal (`m`, `n`, `ng` — treat `ng` as **1 unit** for position counting).
3. **Compound vowels** → mark the **2nd letter from the right** (treating `ng` as 1 unit).
   - **Exception 1**: If the 2nd-from-right letter is `i` → mark the **1st (rightmost)** letter instead.
   - **Exception 2**: **Checked syllable** (stop coda `-p`/`-t`/`-k`) + 2nd-from-right is `i` or `u` (but **not** `iu` / `iu`+stop) → mark the **3rd letter** from the right. (In Hak-fa Si-yen this exception is **vestigial** — inherited from Taigi POJ; standard Si-yen syllables do not produce a 2-vowel checked syllable with `i`/`u` as 2nd-from-right outside the `iu`+stop pattern covered by Special.)
   - **Special**: `iu`+stop → mark **2nd-from-right** (no exception fires; e.g. `liu̍k`).

Hak-fa-specific notes:

- **`ⁿ` does not occur** in Si-yen, so POJ's "skip ⁿ" clause is moot.
- **`ṳ` (numeric `ii`)** is treated as plain `u` for *position counting*. The trema-below (U+0324) is preserved under the tone diacritic via NFC stacking: `u` + U+0324 + tone-combining → e.g. `ṳ̂`. Canonical NFC ordering places U+0324 before tone diacritics (U+0302 / U+0300 / U+0301 / U+030D).
- **Checked codas** in Hak-fa are `-p` / `-t` / `-k` (no `-h` as in Taigi POJ).
- **Syllabic nasals**: `m` is well attested (e.g. negative 唔 → `m̀`). For syllabic `ng` (e.g. 五 / 魚 → `ǹg`), Rule 2 marks the leading letter (`n` in `ng`), since `ng` is treated as one positional unit but the combining diacritic must attach to a single base codepoint. Syllabic `n` is rare in Si-yen — handle case-by-case.
- **PFS y-onglide convention (zero-onset)**: A zero-initial syllable whose rhyme begins with `i` followed by `a`, `e`, `o`, or `u` is written with leading `y` in PFS Unicode/Input: 油 `yû`, 羊 `yông`, 鹽 `yâm`, 也 `yâ`. The bare `i`, the close-central `ii`/`ṳ`, and `i`+nasal-coda (`im`, `in`) keep the `i`. **Tone-mark placement uses the underlying `i`-onglide form for position counting** (apply the placement rule first against the `iV…` shape, then render the leading `i` → `y` on output); reverse direction strips the `y` back to `i` before parsing. Reference: `Pfs.kt:160-163`.

### Worked examples (Hak-fa Si-yen)

`ng` is treated as 1 letter-unit for the position count.

| Syllable | Letter units (ng as 1) | 2nd-from-right | Rule fired | Marked output |
|:---|:---|:---|:---|:---|
| `sî`    | s,i           | (single vowel) | Rule 1 | `sî` |
| `khua`  | k,h,u,a       | `u` | Rule 3 default | `khúa` |
| `koai`  | k,o,a,i       | `a` | Rule 3 default | `koái` |
| `kuai`  | k,u,a,i       | `a` | Rule 3 default | `kuái` |
| `khoan` | k,h,o,a,n     | `a` | Rule 3 default | `khoán` |
| `koet`  | k,o,e,t       | `e` | Rule 3 default | `koét` / `koe̍t` |
| `liang` | l,i,a,**ng**  | `a` | Rule 3 default | `liâng` |
| `siong` | s,i,o,**ng**  | `o` | Rule 3 default | `siông` |
| `sia`   | s,i,a         | `i` | Exception 1 → rightmost | `siá` |
| `liu`   | l,i,u         | `i` | Exception 1 → rightmost | `liù` |
| `kui`   | k,u,i         | `u` | Rule 3 default | `kúi` |
| `liuk`  | l,i,u,k       | `u` (and is checked, vowels=`iu`) | Special (`iu`+stop) → 2nd-from-right | `liu̍k` |
| `hak`   | h,a,k         | (single vowel) | Rule 1 | `ha̍k` (PFS 5) / `hak` (PFS 6) |
| `ng`    | **ng**        | — | Rule 2 (no vowel) | `ǹg` (combining attaches to `n`) |
| `m`     | m             | — | Rule 2 (no vowel) | `m̀` |
| `sṳ`    | s,u (+U+0324) | `u` | Rule 1 (single vowel) | `sṳ̂` (NFC stack) |

> **Key change from the older "nucleus" heuristic**: `iu` is marked on `u` (`liù`, `niù`), **not** on `i`. This matches the FHL dictionary corpus and POJ Section 21. The "syllabic nucleus" framing from some PFS pedagogy produces incorrect output here.

> **Case preservation**: Tone-mark placement is independent of case. Combine the diacritic with the appropriate vowel and preserve the original letter case of the base.

---

## 3. PFS Phoneme Inventory (Si-yen)

### Initials

| PFS         | IPA  | Notes |
|:------------|:-----|:------|
| p           | p    | unaspirated |
| ph          | pʰ   | aspirated |
| m           | m    |  |
| f           | f    |  |
| v           | ʋ    | labio-dental approximant; **not** `v` (fricative). Some sources transcribe as `v` for typographic convenience. |
| t           | t    | unaspirated |
| th          | tʰ   | aspirated |
| n           | n    |  |
| l           | l    |  |
| ch (or ts)  | ts   | unaspirated; modern Taiwan PFS (FHL, 客語聖經) uses `ch`; older missionary-era (Basel, MacIver) used `ts` |
| chh (or tsh)| tsʰ  | aspirated; modern Taiwan PFS uses `chh`; older missionary-era used `tsh` |
| s           | s    |  |
| k           | k    | unaspirated |
| kh          | kʰ   | aspirated |
| ng          | ŋ    |  |
| h           | h    |  |
| (∅)         | —    | zero onset |

### Palatalization Before `/i/` (apply before general initial mapping)

| PFS onset + i  | IPA   |
|:---------------|:------|
| ch(i)  / ts(i) | tɕi   |
| chh(i) / tsh(i)| tɕʰi  |
| s(i)           | ɕi    |
| ng(i)          | ɲi    |

This step is mandatory for phonetically correct Si-yen IPA. Without it, alveolar onsets before `/i/` produce wrong transcriptions.

### Vowels

| PFS  | IPA  | Notes |
|:-----|:-----|:------|
| a    | a    |  |
| e    | e    |  |
| i    | i    |  |
| o    | o    |  |
| u    | u    |  |
| ṳ    | ɨ    | close central unrounded; some sources use `ɿ` (apical); pin one convention per project |
| er   | ɤ    | mid-back unrounded; appears in a small set of Si-yen forms |

### Codas

| PFS    | IPA  | Notes |
|:-------|:-----|:------|
| -m     | m    |  |
| -n     | n    |  |
| -ng    | ŋ    |  |
| -p     | p̚   | unreleased |
| -t     | t̚   | unreleased |
| -k     | k̚   | unreleased |

### Syllabic nasals

`m` is the well-attested syllabic nasal in Si-yen (e.g. negative 唔 → `m̀` → IPA `m̩˩˩`). Syllabic `n` and `ng` as standalone tone-bearing forms are not generally productive in Si-yen — handle on a case-by-case basis.

| PFS  | IPA  | Notes |
|:-----|:-----|:------|
| m    | m̩   | well attested |
| n    | n̩   | rare as standalone syllable |
| ng   | ŋ̍   | rare as standalone syllable |

---

## 4. PFS ↔ KPPY Mapping (Si-yen)

| Feature                  | PFS               | KPPY              |
|:-------------------------|:------------------|:-------------------|
| Voiceless unaspirated    | `p` `t` `k`       | `b` `d` `g`       |
| Voiceless aspirated      | `ph` `th` `kh`    | `p` `t` `k`       |
| Affricate (unaspirated)  | `ts`              | `z`               |
| Affricate (aspirated)    | `tsh`             | `c`               |
| Sibilant                 | `s`               | `s`               |
| Voiced labio-dental      | `v`               | `v`               |
| Velar nasal              | `ng`              | `ng`              |
| Glottal                  | `h`               | `h`               |
| Close central vowel      | `ṳ` (u + U+0324)  | `ii`              |
| Rising u-onglide medial  | `oV` (`oa`, `oai`, `oan`, `oang`, `oat`, `oak`, `oe`, `oen`, `oet`) | `uV` (`ua`, `uai`, `uan`, `uang`, `uad`, `uag`, `ue`, `uen`, `ued`) |
| Final stops              | `-p` `-t` `-k`    | `-b` `-d` `-g`    |
| Syllable boundary        | `-` (hyphen)      | ` ` (space)       |

> **Rising u-onglide caveat**: PFS writes the rising medial `[u]` onglide uniformly as `oV` (瓜 kôa, 關 koân, 怪 koái, 國 koet), where KPPY (and the library's internal canonical form) writes `uV` (gua, guan, guai, gued). **Only `oa-` and `oe-` shift** — bare PFS `o-` is a different rhyme. KPPY's `oi` (愛 oi, /oi/) is also a distinct rhyme, not a shifted form of PFS `oi`. Implementation reference: `Pfs.kt:106-107` (input fold) and `Pfs.kt:153-154` (render).

### KPPY tone numbering — 八聲 調號 (1–8)

The KPPY system uses the traditional eight-tone (八聲) framework. In Si-yen, tones 6 (陽上) and 7 (陽去) are merged, leaving slots **{1, 2, 3, 4, 5, 8}**. The MOE dictionary displays tones using three modes (see §1 "KPPY Three Display Modes"):

1. **調號** — the 八聲 slot number
2. **調型 (符號式)** — modifier-letter diacritics placed after the syllable
3. **調值 (數字式)** — Chao pitch values appended to each syllable

### KPPY tone markers (調型)

KPPY uses **modifier letters placed after the syllable** (not combining diacritics on vowels like PFS). Listed by 調號, with MOE 調類 names and si/sek examples:

- 調號 1 (陰平, PFS 1): ˊ (U+02CA) — e.g. siˊ (調值 ²⁴)
- 調號 2 (上聲, PFS 3): ˋ (U+02CB) — e.g. siˋ (調值 ³¹)
- 調號 3 (去聲, PFS 4): (unmarked) — e.g. si (調值 ⁵⁵)
- 調號 4 (陰入, PFS 6): ˋ on stop-final syllable — e.g. segˋ (調值 ²)
- 調號 5 (陽平, PFS 2): ˇ (U+02C7) — e.g. siˇ (調值 ¹¹)
- 調號 8 (陽入, PFS 5): (unmarked) on stop-final syllable — e.g. seg (調值 ⁵)

> **Note on the library convention**: the KonvertToPFS library does **not** use these 八聲 調號 digits for `KPPY_INPUT`; it uses 1–6 PFS-aligned digits instead (T5 = 陽入, T6 = 陰入). See §1 "MOE 調號 vs KonvertToPFS KPPY digit" for the crosswalk.

KPPY accepts **three input forms** for tone marks on the rhyme, all folded to the modifier-letter canonical form on render:

1. **Modifier letters** appended after the syllable (canonical): `gaˊ` / `gaˇ` / `gaˋ` (U+02CA / U+02C7 / U+02CB).
2. **NFD combining marks** on the rhyme vowel: `a` + U+0301 / U+030C / U+0300 — visually indistinguishable from the modifier letters but encoded as combining diacritics on the nucleus.
3. **Latin precomposed accents** on the rhyme vowel: `á` / `ǎ` / `à` (and the `e`/`i`/`o`/`u` equivalents) — convenient for keyboard layouts that produce them by default.

Reference: `Kppy.kt:30-32` (NFD combining-mark constants), `Kppy.kt:parseUnicode` (decoding branches).

### KPPY numbering caveats

- The MOE dictionary uses two numeric display modes that look similar but are distinct:
  - **調號 (八聲)** — 1, 2, 3, 4, 5, 8 — the tone category number.
  - **調值 (Chao pitch)** — ²⁴, ¹¹, ³¹, ⁵⁵, ⁵, ² — the pitch contour, appended as superscript to each syllable in the 數字式 display.
  Do not mix them without explicit labelling. The single-digit checked-tone 調值 (⁵ and ²) are easily confused with 調號 values.
- KPPY adds initials (`bb`, `rh`, etc.) for non-Si-yen dialects. These are out of scope for default Si-yen conversion — flag and confirm before processing.

---

## 5. IPA Conventions (This Skill)

- **Tone**: Use Chao tone-letter codepoints (U+02E5 ˥ … U+02E9 ˩). Place at end of syllable, after segmental IPA. Do not substitute superscript digits or Latin numerals.
- **Aspiration**: Mark with U+02B0 (modifier letter small h) — `pʰ`, `tʰ`, `kʰ`, `tsʰ`.
- **Unreleased stops**: Mark with U+031A (combining left angle above) — `p̚`, `t̚`, `k̚`. If a project decides to omit unreleased marks, do so consistently.
- **Output formatting**: Two common forms — bare (`pʰak̚˨ fa˥˥ sɨ˥˥`) or per-syllable bracketed (`[pʰak̚˨] [fa˥˥] [sɨ˥˥]`). The HakkaFHLDictDataMirror project's scraper uses the bracketed form. Pin one per project.
- **Pipeline order**: NFC-normalize → segment syllables (by hyphen for PFS/FHL, by space for KPPY) → decode tone digit/diacritic → apply **palatalization** (alveolar+`i` → alveolo-palatal) → apply general initial / vowel / coda mapping → re-attach tone letter.
- **Citation form only** — no tone sandhi is applied; see §6.
- **Reverse direction (IPA → PFS/KPPY) is lossy** — flag any such conversion as approximate.

---

## 6. Tone Sandhi: Out of Scope

Hak-fa Si-yen has well-known sandhi patterns (e.g. PFS 2 ˩˩ → ˧˥ before some following tones; PFS 5 / PFS 6 sandhi in compounds). These depend on prosodic boundaries that this skill does not analyse.

**Rules for IPA output:**

- Each syllable receives the citation tone from §1.
- Concatenate using the project's chosen separator (hyphen, space, or none).
- Never modify a syllable's tone letter based on neighbouring syllables.

If a downstream consumer needs sandhi'd IPA (TTS, prosodic analysis), apply sandhi as a separate post-processing pass outside this skill.

---

## 7. Validation Rules

A syllable is well-formed if **all** of the following hold:

1. Onset (or zero onset) is in the PFS initial inventory (§3).
2. Nucleus is a valid vowel or syllabic nasal.
3. Coda is in the PFS coda inventory or absent.
4. Tone is consistent with the coda:
   - **Stop coda** (`-p` / `-t` / `-k`) → tone must be PFS 5 or PFS 6.
   - **Non-stop coda or open syllable** → tone must be one of PFS 1 / 2 / 3 / 4.
5. For FHL IME input: validate as PFS-numeric (digit must be one of `{1, 2, 3, 4, 5, 6}`).
6. For FHL dict-numeric input: digit must be one of `{1, 2, 3, 4, 5, 8}`. POJ tone 7 does not occur in Si-yen Hakfa data — flag as invalid.
7. For PFS-numeric input: digit must be one of `{1, 2, 3, 4, 5, 6}`.
8. For KPPY-numeric input: determine whether the source uses 調號 (八聲 slots: `{1, 2, 3, 4, 5, 8}`) or 調值 (Chao pitch: `{²⁴, ¹¹, ³¹, ⁵⁵, ⁵, ²}`). Map to PFS via the §1 crosswalk table. The single-digit checked-tone 調值 (⁵ and ²) are easily confused with 調號 values — confirm the convention before transcoding.

---

## 8. Edge Cases

- **Syllable separators**: PFS uses `-` (hyphen) between syllables of a polysyllabic word, and space between words. KPPY uses spaces between all syllables (no hyphens). Preserve each system's convention during round-trips.
- **Capitalization**: Tone-mark placement is independent of case; combine the diacritic with the appropriate vowel and preserve the original letter case.
- **Punctuation**: Han-Lo formatting (full-width/half-width punctuation around Hanji) is handled by separate Han-Lo formatter skills. This skill should not silently reformat punctuation.
- **Foreign words / loans**: PFS texts occasionally contain non-PFS-conformant strings (e.g. proper nouns). Validation should distinguish "non-PFS syllable" from "malformed PFS" — typically by whitelist or regex of PFS-shaped tokens.
- **Mixed scripts**: A line may mix Hanji and PFS. Process Roman segments only; pass Hanji through unchanged.

---

## 9. FHL Dictionary Data — Specifics & Known Divergences

This section documents the empirical conventions of the [台語信望愛客語辭典 (Hak-fa FHL Dictionary)](https://hakka.fhl.net/dict/index_hakka.html) and the published data mirror at [ThoivanHakfa/HakkaFHLDictDataMirror](https://github.com/ThoivanHakfa/HakkaFHLDictDataMirror). Use this when ingesting or converting FHL data.

### 9.1 FHL Dict ↔ PFS Numeric Conversion

FHL serves Hak-fa numerics in **POJ-style digits** (only `{2, 3, 5, 8}` are marked; `{1, 4}` are omitted from the surface form). The canonical mapping to PFS 1–6 is:

| FHL dict digit | Surface | PFS # | Coda condition |
|:--------------:|:-------:|:-----:|:---------------|
| `5` (marked)   | `si5`   | **1** (sî, ˆ)             | open / nasal |
| `3` (marked)   | `si3`   | **2** (sì, ` )            | open / nasal |
| `2` (marked)   | `si2`   | **3** (sí, ´)             | open / nasal |
| (omitted)      | `si`    | **4** (si, unmarked)      | open / nasal coda |
| `8` (marked)   | `sek8`  | **5** (se̍k, ◌̍ + stop)    | stop coda `-p`/`-t`/`-k` |
| (omitted)      | `sek`   | **6** (sek, unmarked + stop) | stop coda `-p`/`-t`/`-k` |

**Marked-digit map**: `{5→1, 3→2, 2→3, 8→5}`.

**Unmarked disambiguation by coda**: open or nasal coda → PFS 4; stop coda (`-p` / `-t` / `-k`, case-insensitive) → PFS 6.

> **Idempotency warning**: Roughly 12% of real FHL rows are structurally indistinguishable from valid PFS in isolation (the `(open, 2)` / `(open, 3)` collision — e.g. `ham3` is valid as both FHL `hàm` and PFS `hám`). **Never auto-detect input form per-row.** For idempotent bulk re-conversion, gate the call with a corpus-level form detector (see `is_pfs_numeric_corpus()` in the mirror's `script/scraper.py`): treat the whole file as FHL form iff every entry consists of valid PFS shapes; otherwise assume FHL.

> **Tone 7 does not occur** in Si-yen Hak-fa FHL data. Encountering a `7` digit indicates upstream drift — flag as invalid.

### 9.2 FHL `graph=0` vs `graph=2` Columns

The FHL site exposes each entry in two encodings via query parameter:

- **`graph=0`** — `FHL_DICT_Numeric` (POJ-style 1–8 digits)
- **`graph=2`** — `FHL_DICT_Unicode` (combining-diacritic display form)

The two are not perfectly round-trip equivalent — see §9.3 (placement) and §9.4 (`ṳ` handling) below.

### 9.3 FHL's Empirical Tone-Mark Placement vs Canonical POJ

The FHL `graph=2` column does **not** strictly follow POJ Section 21. Empirically (validated across ~30,420 marked syllables), FHL places the diacritic on the **first vowel of the vowel cluster**, skipping a leading medial `i`. This matches canonical POJ on **open** syllables but diverges on **closed** syllables and `-ai` triphthongs.

**Divergence cells** — 52 syllables across the entire corpus need repositioning to match canonical POJ:

| Vowel cluster | FHL marks (1st vowel) | Canonical POJ marks (2nd from right) | Example (FHL → canonical) | Corpus count |
|:-------------:|:---------------------:|:------------------------------------:|:--------------------------|:------------:|
| `oai`         | `o` (1st)             | `a` (2nd of 3)                       | `kóai` → `koái`           | 16 |
| `uai`         | `u` (1st)             | `a` (2nd of 3)                       | `kúai` → `kuái`           | 1  |
| `oa`+coda     | `o` (1st vowel)       | `a` (2nd letter from right)          | `khòan` → `khoàn`; `khôang` → `khoáng` | 31 |
| `oe`+coda     | `o` (1st vowel)       | `e` (2nd letter from right)          | `ko̍et` → `koe̍t`         | 2  |
| `ua`+coda     | `u` (1st vowel)       | `a` (2nd letter from right)          | `kûan` → `kuân`; `ngùan` → `nguàn` | 2  |

**Total: 52 syllables.** All other clusters — `khúa`, `khôa`, `koa`, `liù`, `kúi`, `siá`, `liâng`, `siông`, `iau`/`ieu` triphthongs, `iu`+stop, syllabic `ng`/`m`, `ṳ`-bearing syllables — already match canonical POJ in FHL's output and pass through unchanged.

**When converting FHL → canonical PFS**:

- Preserve `FHL_DICT_Unicode` verbatim in any "raw" / `tangloo/` column for traceability.
- Reposition per §2 (POJ Section 21) for the derived / `bunji/` `PFS_Unicode` column.
- The mirror's `script/scraper.py` exposes `_reposition_syllable()` and `fhl_unicode_to_pfs_unicode()` as a reference implementation.

### 9.4 `ṳ` (Trema-Below) Restoration

FHL's `graph=2` column **drops the combining diaeresis-below (U+0324)** from `ṳ` whenever a tone diacritic is added. Example: numeric `sii5` → FHL Unicode `sû` (missing trema), rather than the correct `sṳ̂`.

The numeric column `graph=0` always spells the close-central vowel as `ii`, so it is the **authoritative source** for restoring U+0324. The restoration algorithm:

1. Decompose both forms to NFD; segment syllables.
2. For each aligned pair, walk the numeric base letter-by-letter against the Unicode base.
3. Whenever numeric `ii` aligns with a Unicode `u` that lacks U+0324, append U+0324 at that position.
4. Reassemble in canonical NFC order (U+0324 before tone diacritics).

> The mirror's `_reposition_syllable()` is **defensive** about this — on current FHL snapshots, FHL actually preserves U+0324 for *un-toned* `ṳ` (e.g. `sṳ`) and only drops it under a tone diacritic, so the restoration only fires on toned forms. Do not assume FHL data is uniformly U+0324-free.

### 9.5 Data Schema (HakfaFHLDictDataMirror, `bunji/` derived output)

The mirror's `bunji/HakfaFHLDict.csv` is the recommended starting point for Hak-fa NLP, since it normalises to PFS 1–6 and canonical POJ tone-mark placement:

| Column            | Description                                                            |
|:------------------|:-----------------------------------------------------------------------|
| `ID`              | FHL database ID                                                        |
| `FHL_DICT_Numeric`| Original FHL (POJ-style digits 1–8), retained for traceability         |
| `PFS_Numeric`     | PFS 1–6 numeric (derived via §9.1 mapping)                             |
| `PFS_Unicode`     | PFS Unicode with **canonical POJ Section 21 placement** and restored `ṳ` (differs from `FHL_DICT_Unicode` on the 52 divergence cells in §9.3) |
| `Hakfa_IPA`       | IPA with Chao tone letters, **per-syllable bracketed** form            |
| `Hanzi`, `Tai-gi`, `Hakfa-exp`, `Hua-gi`, `Eng-gi` | 漢字 / Taigi / Hak-fa / Mandarin / English glosses |

KPPY columns are intentionally **omitted** from `bunji/`. For PFS ↔ KPPY ↔ IPA conversion at scale, the mirror points to its Kotlin Multiplatform sibling library `lib/KonvertToPFS` (GPL-3.0).

### 9.6 Pitfalls When Working With FHL Data

1. **FHL IME ≠ FHL dict numbering.** The FHL **input method** (信望愛客語輸入法) uses PFS-style 1–6 (no renumbering needed). Only the FHL **dictionary website** uses the POJ-style 1–8 digits in this section. Confirm the source before applying §9.1.
2. **Per-row form detection is unsafe.** Use the corpus-level detector — see §9.1 idempotency warning.
3. **The 52 divergence-cell syllables look correct in FHL Unicode.** They are valid PFS letter-strings with valid diacritics, just placed on the wrong vowel. Without an explicit canonical reference, naive PFS validators will not flag them.
4. **Tone diacritic ≠ stop coda for PFS 5 / 6 disambiguation.** Both `se̍k` (PFS 5) and `sek` (PFS 6) have a stop coda; the difference is the U+030D vertical line on `e`. Don't conflate "has stop coda" with "is checked tone 5".
5. **Don't reverse FHL → PFS digit conversion blindly.** A `5` in FHL means PFS 1 (circumflex), but a `5` in PFS means PFS 5 (vertical-line stop). See §1 "Why FHL dict ↔ PFS renumbering is a trap".

---

## 10. Comprehensive Initial and Final Inventory (Si-yen / Nam-Si-yen)

Source: Taiwan MOE *Hakfa Phonetic Scheme User Manual* (2012), §2.2 (initial-symbol usage notes), §2.3 (final-symbol usage notes), and §2.4 (cross-dialect initial / final comparison table), with the appendix syllable tables for Si-yen (pp. 15–37) and Nam-Si-yen (pp. 141–). Cross-checked against the [KonvertToPFS](https://github.com/Phakfasu/KonvertToPFS) Kotlin Multiplatform reference implementation.

Tables here use **KPPY orthography as the anchor** (the library's internal canonical form) with the **PFS** column showing the Pha̍k-fa-sṳ equivalent and **IPA** giving the phonetic value. Si-yen and Nam-Si-yen share an identical initial inventory; finals differ on exactly two cells (`ian`, `iad` — see §10.4).

### 10.1 Initials (Si-yen / Nam-Si-yen)

| KPPY | PFS      | IPA  | Si-yen | Nam-Si-yen | KPPY examples |
|------|----------|------|:------:|:----------:|:--------------|
| ø    | (none)   | ∅    | ✓ | ✓ | a-阿亞, ai-哀矮, on-安鞍, iu-油又 |
| b    | p        | [p]  | ✓ | ✓ | ba-巴爸, bun-本笨, bi-比筆 |
| p    | ph       | [pʰ] | ✓ | ✓ | pa-怕爬, pun-噴盆, pi-皮鼻 |
| m    | m        | [m]  | ✓ | ✓ | ma-媽馬, mun-悶問, mi-米眯 |
| f    | f        | [f]  | ✓ | ✓ | fa-花化, fun-分粉, fi-□ |
| v    | v        | [ʋ]  | ✓ | ✓ | va-蛙娃, vun-溫穩, vi-位胃 |
| d    | t        | [t]  | ✓ | ✓ | da-打, dun-敦頓, di-知帝 |
| t    | th       | [tʰ] | ✓ | ✓ | ta-他塔, tun-吞屯, ti-提弟 |
| n    | n        | [n]  | ✓ | ✓ | na-拿那, nun-嫩, ni-□ (palatalised to ngi) |
| l    | l        | [l]  | ✓ | ✓ | la-拉, lun-論輪, li-梨利 |
| z    | ch (ts)  | [ts] | ✓ | ✓ | za-渣榨, zun-準遵, zii-資子 |
| c    | chh (tsh)| [tsʰ]| ✓ | ✓ | ca-差查, cun-村寸, cii-次詞 |
| s    | s        | [s]  | ✓ | ✓ | sa-沙紗, sun-孫損, sii-私士 |
| j    | ch (ts)  | [tɕ] | ✓ | ✓ | ji-知支 (allophone of z before i) |
| q    | chh (tsh)| [tɕʰ]| ✓ | ✓ | qi-妻欺 (allophone of c before i) |
| x    | s        | [ɕ]  | ✓ | ✓ | xi-西犀 (allophone of s before i) |
| g    | k        | [k]  | ✓ | ✓ | ga-家加, gun-滾棍, gi-居佢 |
| k    | kh       | [kʰ] | ✓ | ✓ | ka-卡, kun-綑捆, ki-企其 |
| ng   | ng       | [ŋ]  | ✓ | ✓ | nga-牙瓦, ngo-鵝餓, ngi-蟻 (→ [ɲ]) |
| h    | h        | [h]  | ✓ | ✓ | ha-蝦下, hun-訓婚, hi-去戲 |

#### KPPY ↔ PFS initial differences (compact crosswalk)

Eight KPPY initial letters spell their PFS equivalents differently. The shift is **systematic**: KPPY uses voiced letters for voiceless unaspirated stops and reserves the bare voiceless letter for the aspirated counterpart.

| KPPY | PFS           | Note |
|------|---------------|------|
| `b`  | `p`           | Voiceless unaspirated stop; KPPY uses the voiced-letter convention. |
| `p`  | `ph`          | Aspirated stop; PFS marks aspiration with `h`. |
| `d`  | `t`           | Voiceless unaspirated stop. |
| `t`  | `th`          | Aspirated stop. |
| `g`  | `k`           | Voiceless unaspirated stop. |
| `k`  | `kh`          | Aspirated stop. |
| `z`  | `ch` (`ts`)   | Affricate; PFS accepts both traditional `ch` and modern `ts` on input, renders `ch`. |
| `c`  | `chh` (`tsh`) | Aspirated affricate; PFS accepts both `chh` and `tsh`, renders `chh`. |

> **Pitfall**: A naïve letter-for-letter swap silently inverts aspiration. PFS `pa` (unaspirated) → KPPY `ba`, but PFS `pha` (aspirated) → KPPY `pa`. Always apply the table above.

#### Allophonic j / q / x before i

KPPY uses `j q x` as the alveolo-palatal allophones of `z c s` before the high front vowel `i` (but **not** before the apical vowel `ii` = PFS `ṳ`). PFS does not orthographically distinguish them — `ji`, `qi`, `xi` all render the same affricate/sibilant letters (`chi`, `chhi`, `si`) as before any other vowel. Conversion libraries normalise `j q x` → `z c s` internally and restore them on KPPY output when the rhyme begins with `i` (not `ii`).

| KPPY  | Internal | KPPY render | PFS render | IPA   |
|-------|----------|-------------|------------|-------|
| `ji`  | `zi`     | `ji`        | `chi`      | [tɕi] |
| `qi`  | `ci`     | `qi`        | `chhi`     | [tɕʰi]|
| `xi`  | `si`     | `xi`        | `si`       | [ɕi]  |
| `zii` | `zii`    | `zii`       | `chṳ`      | [tsɨ] |
| `cii` | `cii`    | `cii`       | `chhṳ`     | [tsʰɨ]|
| `sii` | `sii`    | `sii`       | `sṳ`       | [sɨ]  |

#### Initials — notes

- **Zero initial (ø)**: syllables beginning with a vowel have no initial consonant. Common with finals `a, ai, au, e, eu, i, o, oi, on, u, un, iu`, etc.
- **`v` realisation**: Si-yen `v` is a labio-dental approximant [ʋ], not the fricative [v].
- **`ng` palatalisation**: `ng` before `i` palatalises to [ɲ] (e.g. `ngi` → [ɲi]).
- **`n` before `i`**: largely merged into `ng` (→ [ɲ]) in Si-yen; standalone `ni` is rare.
- **Syllabic nasals**: `m`, `n`, `ng` may stand alone as syllables (no rhyme) — see §10.3.

### 10.2 Finals (Si-yen / Nam-Si-yen)

Finals are organised by coda type. Checked finals carry tones 5/6 only. The five finals built on the apical vowel **ii** (`ii, iim, iin, iib, iid`) occur only in Si-yen and Nam-Si-yen — they are absent from Hai-liu, Tai-pu, Rau-ping, and Zhao-an (MOE note 16).

> **Peripheral rhyme not in the tables below**: the open rhyme `er` ([ɤ], mid-back unrounded — see §3 Vowels) appears in a small number of Si-yen forms but is not part of the MOE syllable-table inventory and is omitted from the cells here. Treat `er` as a legal but uncommon nucleus when validating; do not expect it in MOE-derived data.

> **Reading the KPPY ↔ PFS cells**: the KPPY `u*` → PFS `o*` correspondences below (`ua→oa`, `uai→oai`, `uan→oan`, `uang→oang`, `uad→oat`, `uag→oak`, `ue→oe`, `uen→oen`, `ued→oet`) all follow a single systematic rule: PFS writes the rising u-onglide as `oV`, KPPY writes it as `uV`. Only the **medial-`u`** finals shift — bare PFS `o-` and PFS `oi` are distinct rhymes that **do not** correspond to KPPY `u-`. See §4 "Rising u-onglide caveat" for the full rule.

#### Open finals

| KPPY | PFS | IPA | Si-yen | Nam-Si-yen | KPPY examples |
|------|-----|-----|:------:|:----------:|:--------------|
| a    | a   | [a]   | ✓ | ✓ | b-爸把, m-媽罵, d-打 |
| o    | o   | [o]   | ✓ | ✓ | g-哥高, s-嫂掃, d-多倒 |
| e    | e   | [e]   | ✓ | ✓ | m-姆, h-係, s-細 |
| ii   | ṳ   | [ɨ]   | ✓ | ✓ | z-資子, c-次詞, s-私士 |
| i    | i   | [i]   | ✓ | ✓ | d-知帝, g-居佢, k-企其 |
| u    | u   | [u]   | ✓ | ✓ | d-都肚, t-涂度, f-呼腐 |
| ai   | ai  | [ai]  | ✓ | ✓ | z-災債, c-採猜, s-晒徙 |
| au   | au  | [au]  | ✓ | ✓ | b-包豹, p-跑刨, m-矛貌 |
| eu   | eu  | [eu]  | ✓ | ✓ | ø-歐漚, d-斗鬥, h-候侯 |
| oi   | oi  | [oi]  | ✓ | ✓ | b-背, p-賠, m-妹 |
| ia   | ia  | [ia]  | ✓ | ✓ | d-踩, p-跛, ng-惹 |
| ie   | ie  | [ie]  | ✓ | ✓ | g-計解, k-契乞, ng-蟻艾 |
| io   | io  | [io]  | ✓ | ✓ | k-癰, ng-揉, h-靴 |
| iu   | iu  | [iu]  | ✓ | ✓ | d-丟, l-流柳, k-久救 |
| iau  | iau | [iau] | ✓ | ✓ | ø-柺, h-曉, ng-攬 |
| ieu  | ieu | [ieu] | ✓ | ✓ | g-鉤溝, k-摳扣, ng-偶藕 |
| ioi  | ioi | [ioi] | ✓ | ✓ | 痠 (Si-yen); MOE note 20 marks this final as limited |
| ua   | oa  | [ua]  | ✓ | ✓ | g-瓜掛, k-誇 (☆ Si-yen lacks `ngua` — MOE note 19) |
| uai  | oai | [uai] | ✓ | ✓ | g-乖怪, k-快 |
| ui   | ui  | [ui]  | ✓ | ✓ | g-鬼貴, d-追, l-類雷 |
| ue   | oe  | [ue]  | ✓ | ✓ | k-口 (no grapheme) |

#### Bilabial nasal coda (-m)

| KPPY | PFS | IPA | Si-yen | Nam-Si-yen | KPPY examples |
|------|-----|-----|:------:|:----------:|:--------------|
| am   | am  | [am]   | ✓ | ✓ | f-范凡, d-擔膽, l-藍覽 |
| em   | em  | [em]   | ✓ | ✓ | z-砧, c-岑, s-森參 |
| im   | im  | [im]   | ✓ | ✓ | g-金, k-欽, h-歆 |
| iim  | ṳm  | [ɨm]   | ✓ | ✓ | z-斟枕, c-深沉, s-沈甚 |
| iam  | iam | [iam]  | ✓ | ✓ | g-兼劍, k-欠謙, ng-驗嚴 |
| iem  | iem | [iem]  | ✓ | ✓ | g-□, k-□, ng-□ (no graphemes) |

#### Alveolar nasal coda (-n)

| KPPY | PFS | IPA | Si-yen | Nam-Si-yen | KPPY examples |
|------|-----|-----|:------:|:----------:|:--------------|
| an   | an  | [an]   | ✓ | ✓ | b-班半, d-單旦, z-贊盞 |
| en   | en  | [en]   | ✓ | ✓ | ø-恩應, z-曾贈, d-丁等 |
| in   | in  | [in]   | ✓ | ✓ | b-兵併, g-斤緊, ng-人認 |
| iin  | ṳn  | [ɨn]   | ✓ | ✓ | z-真蒸, c-稱神, s-勝甚 |
| ien  | ien | [ien]  | ✓ | ✓ | b-編扁, g-見揭, ng-願原 |
| ian  | ian | [ian]  | ✗ | ✓ | **Nam-Si-yen only** (after velar / zero initial — MOE note 22). Si-yen merges these into **ien** |
| on   | on  | [on]   | ✓ | ✓ | ø-安鞍, g-乾干, d-端短 |
| ion  | ion | [ion]  | ✓ | ✓ | q-/c-吮全 |
| un   | un  | [un]   | ✓ | ✓ | b-本, t-屯吞, z-俊 |
| iun  | iun | [iun]  | ✓ | ✓ | g-君僅, k-裙近, ng-勒 |
| uan  | oan | [uan]  | ✓ | ✓ | g-關慣, k-款環, ng-頑玩 |
| uen  | oen | [uen]  | ✓ | ✓ | g-耿 |

#### Velar nasal coda (-ng)

| KPPY | PFS  | IPA | Si-yen | Nam-Si-yen | KPPY examples |
|------|------|-----|:------:|:----------:|:--------------|
| ang  | ang  | [aŋ]   | ✓ | ✓ | ø-盎, m-猛蕻, g-耕庚 |
| iang | iang | [iaŋ]  | ✓ | ✓ | p-平病, g-驚鏡, l-領 |
| uang | oang | [uaŋ]  | ✓ | ✓ | g-桄莖 |
| ong  | ong  | [oŋ]   | ✓ | ✓ | b-榜幫, d-當擋, l-狼浪 |
| iong | iong | [ioŋ]  | ✓ | ✓ | b-枋放, t-暢, ng-讓娘 |
| ung  | ung  | [uŋ]   | ✓ | ✓ | p-蜂縫, d-東董, s-雙送 |
| iung | iung | [iuŋ]  | ✓ | ✓ | l-龍壟, g-芎拱, k-共 |

#### Bilabial stop coda (KPPY `-b` / PFS `-p`)

| KPPY | PFS | IPA | Si-yen | Nam-Si-yen | KPPY examples |
|------|-----|-----|:------:|:----------:|:--------------|
| ab   | ap  | [ap̚]   | ✓ | ✓ | d-答搭, t-塔踏, h-合盒 |
| eb   | ep  | [ep̚]   | ✓ | ✓ | d-□〔擖〕, l-□〔垃〕, s-澀齕 |
| ib   | ip  | [ip̚]   | ✓ | ✓ | l-立, g-急, k-及 |
| iib  | ṳp  | [ɨp̚]   | ✓ | ✓ | z-汁執, s-濕十 |
| ieb  | iep | [iep̚]  | ✓ | ✓ | g-□〔激〕, k-□〔搦〕 |
| iab  | iap | [iap̚]  | ✓ | ✓ | t-帖墊, l-粒獵, g-挾劫 |

#### Alveolar stop coda (KPPY `-d` / PFS `-t`)

| KPPY | PFS | IPA | Si-yen | Nam-Si-yen | KPPY examples |
|------|-----|-----|:------:|:----------:|:--------------|
| ad   | at  | [at̚]   | ✓ | ✓ | m-抹襪, t-達捷, l-辣 |
| ed   | et  | [et̚]   | ✓ | ✓ | b-北逼, d-德得, z-則仄 |
| id   | it  | [it̚]   | ✓ | ✓ | b-筆必, l-力栗, z-特職 |
| iid  | ṳt  | [ɨt̚]   | ✓ | ✓ | z-質職, c-直姪, s-食失 |
| ied  | iet | [iet̚]  | ✓ | ✓ | b-鱉, g-結蕨, ng-熱月 |
| iad  | iat | [iat̚]  | ✗ | ✓ | **Nam-Si-yen only** (after velar / zero initial — MOE note 24). Si-yen merges these into **ied** |
| od   | ot  | [ot̚]   | ✓ | ✓ | g-割葛, t-脫奪, l-将 |
| iod  | iot | [iot̚]  | ✓ | ✓ | j-/z-噭 |
| ud   | ut  | [ut̚]   | ✓ | ✓ | b-不, f-佛, m-沒歿 |
| iud  | iut | [iut̚]  | ✓ | ✓ | k-屈 |
| uad  | oat | [uat̚]  | ✓ | ✓ | g-刮括 |
| ued  | oet | [uet̚]  | ✓ | ✓ | g-嘓 |

#### Velar stop coda (KPPY `-g` / PFS `-k`)

| KPPY | PFS | IPA | Si-yen | Nam-Si-yen | KPPY examples |
|------|-----|-----|:------:|:----------:|:--------------|
| ag   | ak  | [ak̚]   | ✓ | ✓ | b-伯, t-踢, g-隔 |
| og   | ok  | [ok̚]   | ✓ | ✓ | ø-惡, b-博殼, g-各角 |
| ug   | uk  | [uk̚]   | ✓ | ✓ | b-卜, d-篤督, g-谷穀 |
| iag  | iak | [iak̚]  | ✓ | ✓ | b-壁, g-屐, k-展 |
| iog  | iok | [iok̚]  | ✓ | ✓ | p-縛, l-略掠, ng-弱 |
| iug  | iuk | [iuk̚]  | ✓ | ✓ | l-陸綠, g-菊局, ng-玉肉 |
| uag  | oak | [uak̚]  | ✓ | ✓ | g-□〔聒〕, k-□〔栝〕 (no grapheme) |

### 10.3 Syllabic nasals

| KPPY | PFS | IPA | Si-yen | Nam-Si-yen | Examples |
|------|-----|-----|:------:|:----------:|:---------|
| m    | m   | [m̩]   | ✓ | ✓ | 毋 m̌ (PFS `m̀`, KPPY `mˇ`) |
| n    | n   | [n̩]   | ✓ | ✓ | 嗯 |
| ng   | ng  | [ŋ̍]   | ✓ | ✓ | 魚 ngˇ, 五 ngˇ, 吳 ngˇ |

> Syllabic nasals carry tones 1–4 only — they have no stop coda, so PFS 5/6 are not licensed. In Zhao'an the morphemes 魚/五/吳 are realised as syllabic `m` and 你 as `hen`; Si-yen and Nam-Si-yen do not share that pattern (MOE note 25).

> **Library asymmetry — syllabic `n`**: MOE inventory lists syllabic `n` (嗯) as a Si-yen / Nam-Si-yen form, but the [KonvertToPFS](https://github.com/Phakfasu/KonvertToPFS) parser accepts only `m` and `ng` as standalone-syllable initials (see §10.5 rule 4 and `Kppy.kt:isValidRhyme`). 嗯 is rare and largely interjectional in Si-yen — see §3 Syllabic nasals. When ingesting MOE data, route any syllabic-`n` rows through a separate path or skip them; the library will reject them as malformed.

### 10.4 Si-yen vs Nam-Si-yen — final inventory differences

Nam-Si-yen and Si-yen share an identical final inventory **except** for two finals that Nam-Si-yen introduces after velar (`g, k, ng`) or zero initials:

| Nam-Si-yen final | Si-yen equivalent          | Example (Nam-Si-yen → Si-yen) |
|------------------|----------------------------|-------------------------------|
| **ian** [ian]    | merges into **ien** [ien]   | 願 ngian → ngien |
| **iad** [iat̚]    | merges into **ied** [iet̚]   | 月 ngiad → ngied |

When ingesting MOE Nam-Si-yen syllable tables for Si-yen output, fold `ian`→`ien` and `iad`→`ied` after the velar / zero-initial gate.

### 10.5 KPPY-anchored rhyme inventory (parser perspective)

The [KonvertToPFS](https://github.com/Phakfasu/KonvertToPFS) library uses KPPY as its internal canonical form. A Si-yen rhyme must:

1. Begin with a vowel from `{a, e, i, o, u}` (the close-central vowel ṳ is written `ii`).
2. Contain only characters from `{a, e, i, o, u, r, m, n, g, b, d, p, t, k}` (`r` only in the rare `er` digraph; `p`, `t`, `k` are tolerated as PFS-style stop codas on input but canonicalised to `b`, `d`, `g` internally).
3. Carry a tone consistent with its coda (open / nasal → 1–4; stop coda → 5 or 6).
4. If empty (syllabic nasal), the initial must be `m` or `ng`, and the tone must be 1–4 (5/6 forbidden — no stop coda available).

Letters that **cannot** legally appear in a Si-yen rhyme: `c, f, h, j, l, q, s, v, w, x, y, z`.

---

## 11. KonvertToPFS — Library API & File Map

The [KonvertToPFS](https://github.com/Phakfasu/KonvertToPFS) Kotlin Multiplatform library (GPL-3.0-or-later) is the reference implementation cited throughout this document. This section documents its public API, internal model, and the per-file map between library sources and the skill sections that depend on them.

### 11.1 Public API

```kotlin
package org.phakfasu.konverttopfs

object KonvertToPfs {
    fun convert(text: String, from: LomajiFormat, to: LomajiFormat): String
}
```

Behavioral contract:

- Returns `text` unchanged when `from == to` or input is empty.
- Tokenizes input into word / non-word spans; converts each word independently; passes non-word content (whitespace, punctuation, Hanji, other scripts) through verbatim.
- Per-token casing is detected and reapplied — lowercase, Title-Case, and ALL-CAPS inputs all round-trip.
- Tokens that fail validation (unrecognized letters, out-of-range tone digits, illegal coda+tone combinations, Si-yen-illegal syllabic nasals with checked tones) are emitted **verbatim** — the call is non-destructive on mixed text.
- Compound tokens lacking an explicit separator (e.g. KPPY `ziinˊnaˇ`) are split on syllable-end markers (modifier letters for KPPY_UNICODE, trailing digits for the *_INPUT formats, combining marks for PFS_UNICODE / FHL_UNICODE) and rejoined with a single space. A space is used rather than a hyphen because the joined input gives no signal about word vs compound boundaries.
- `IPA` is **render-only** — invoking `convert(text, IPA, anything)` will not parse the IPA back into a syllable; reverse-mapping IPA → orthography is lossy by design.

Reference: `KonvertToPfs.kt`.

### 11.2 `LomajiFormat` enum

Seven values that map 1:1 to the seven canonical formats this skill enumerates:

| `LomajiFormat`    | Example                | Notes |
|-------------------|------------------------|-------|
| `PFS_INPUT`       | `hak5-ka1-fa4`         | ASCII `ii` for the close-central vowel; trailing 1–6 digit. |
| `PFS_UNICODE`     | `ha̍k-kâ-fa`           | Combining diacritics on the nucleus; `ṳ` (U+1E73 = u + U+0324) for the close-central vowel; both NFC and NFD accepted on input. |
| `KPPY_INPUT`      | `hag5-ga1-fa4`         | **1–6 PFS-aligned digits**, not MOE 八聲 調號 — see §1. |
| `KPPY_UNICODE`    | `hag-gaˊ-fa`           | Modifier letters appended; NFD combining marks and Latin precomposed accents also accepted on input (§4). |
| `FHL_DICT_INPUT`  | `hak8-ka5-fa1`         | POJ-style digits `{1,2,3,4,5,8}` — see §9.1. |
| `FHL_UNICODE`     | `ha̍k-kâ-fa`           | Identical glyphs to `PFS_UNICODE`; library does not implement FHL's `graph=2` placement divergences from canonical POJ (§9.3) — for those, see the mirror's `_reposition_syllable`. |
| `IPA`             | `hak̚˥-ka˨˦-fa˥˥`      | Chao tone letters; render-only; citation tone per syllable (no sandhi, §6). |

Reference: `LomajiFormat.kt`.

### 11.3 `HakfaSyllable` data class (internal model)

```kotlin
data class HakfaSyllable(
    val initial: String,   // KPPY-canonical: z/c/s (allophones j/q/x folded in)
    val rhyme: String,     // KPPY-canonical: "ii" for ṳ; stop codas as b/d/g
    val tone: Int          // 1–6 PFS slot
)
```

- The library's internal canonical form is **KPPY-shaped** (stop codas `b`/`d`/`g`, `"ii"` for the close-central vowel, `z`/`c`/`s` for the affricates).
- `j`/`q`/`x` initials are folded to `z`/`c`/`s` on parse and restored on KPPY render when the rhyme begins with `i` (but not `ii`).
- PFS render unfolds `b`/`d`/`g` back to `p`/`t`/`k`, `"ii"` back to `ṳ`, `z`/`c` back to `ch`/`chh`, and applies the `oV` rising-onglide unfold (§4) and `y` zero-onset onglide rewrite (§2 PFS y-onglide).
- Not part of the public API — `HakfaSyllable` is `internal` to the library.

Reference: `HakfaSyllable.kt`, `Pfs.kt:renderBase`, `Kppy.kt:renderBase`.

### 11.4 File map

Each upstream source file ↔ the skill section it backs:

| File                  | Skill section(s)                                                                                        |
|-----------------------|---------------------------------------------------------------------------------------------------------|
| `KonvertToPfs.kt`     | §11.1 (entry point, tokenization, non-destructive passthrough)                                          |
| `LomajiFormat.kt`     | §11.2 (the seven canonical formats this skill enumerates)                                               |
| `HakfaSyllable.kt`    | §11.3 (internal data model)                                                                             |
| `Pfs.kt`              | §2 (placement), §3 (PFS inventory), §4 (oV↔uV @ lines 106-107 / 153-154), §2 (y-onglide @ lines 160-163)|
| `Kppy.kt`             | §1 (PFS-aligned KPPY digit @ lines 24-29), §4 (KPPY tolerant input @ lines 30-32), §10.3 (syllabic `m`/`ng` only), §10.5 (rhyme inventory) |
| `FhlDict.kt`          | §1 / §9.1 (FHL dict ↔ PFS renumbering)                                                                  |
| `Ipa.kt`              | §5 (IPA conventions, Chao tone letters, palatalization, unreleased-stop marking)                        |
| `SiyenTones.kt`       | §1 (master tone metadata; canonical source for the per-slot ToneInfo records)                           |

### 11.5 License

The library is licensed under **GPL-3.0-or-later**. Any code derived from it inherits the copyleft obligation; this skill is reference documentation only and does not redistribute library code.
