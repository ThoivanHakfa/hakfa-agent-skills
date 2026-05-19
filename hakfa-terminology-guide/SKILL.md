---
name: hakfa-terminology-guide
description: Enforces correct terminology for the Hakfa language and its writing systems. Use this to ensure all communication, documentation, and processing refers to the language as "Hakfa" (or "Hak-fa") and its scripts as "Roman Orthography".
---

# Hakfa Terminology Guide

This skill ensures that all work related to the Hakfa language follows the preferred linguistic terminology.

## Core Rules

1.  **Language Name:** Always refer to the language as **Hakfa** (or **Hak-fa**).
    *   **Avoid:** "Hakka Chinese", "Taiwanese Hakka", "Hakka dialect", or treating Hakfa as a dialect of Mandarin/Chinese.
    *   **Note:** "Hakka" alone is acceptable in widely understood English contexts (e.g. "Hakka people"), but **Hakfa** / **Hak-fa** is preferred when referring to the language itself.
2.  **Terminology:** Use the term **Roman Orthography** (or "Roman Orthography") instead of "Romanization" or "romanization".
3.  **Orthography Names:**
    *   Use **Hakfa Latin-script Orthography** or **Hakfa Roman-script Orthography** as the general term.
    *   Use **PFS (Pha̍k-fa-sṳ)** for the primary Presbyterian-tradition Roman Orthography (the standard used in the FHL Hak-fa Dictionary and in this project's data).
    *   Use **KPPY (Kàu-pō͘ Phin-yîm / 教育部客家語拼音方案)** for the official MOE standard. Full PFS name: Hak-kâ-ngî Phîn-yîm Fông-on.
    *   **Avoid:** "Hakka Romanization", "Hakka Pinyin" (ambiguous), "MOE Pinyin", or conflating PFS with KPPY — they are distinct systems with different consonant inventories and tone-marking conventions.
4.  **Tone Conventions (PFS):**
    *   PFS tone diacritics follow the long-standing 長老教會 (Presbyterian Church) PFS convention.
    *   For numeric tones, use the **traditional 長老教會 PFS tone numbers 1~6** (Si-yen 四縣腔).
    *   **Reference only — do not surface in normal output:** the six PFS numbers correspond to the Chinese tone categories 陰平, 陽平, 上聲, 去聲, 陽入, 陰入 (in that order). 陽入 (PFS 5, e.g. se̍k / 服) is the high-short entering tone (PFS vline + stop, KPPY unmarked + stop, KPPY 調值 5, IPA ˥); 陰入 (PFS 6, e.g. sek / 福) is the low-short entering tone (PFS unmarked + stop, KPPY ˋ + stop, KPPY 調值 2, IPA ˨). This mapping is recorded here for unambiguous identification, but **avoid using these Chinese tone-category labels** in code comments, documentation, user-facing text, or conversation. Refer to tones by their PFS number (1~6) and the canonical example word instead.
    *   **Canonical tone-set example** (Si-yen):

        | PFS # | PFS Diacritic            | PFS Example | KPPY 調號 | KPPY 調型             |
        |:------|:-------------------------|:------------|:----------|:------------------------|
        | 1     | circumflex (â)           | **sî**      | 1 (陰平)  | ˊ (modifier letter)     |
        | 2     | grave (à)                | **sì**      | 5 (陽平)  | ˇ (caron)               |
        | 3     | acute (á)                | **sí**      | 2 (上聲)  | ˋ (modifier letter)     |
        | 4     | (unmarked)               | **si**      | 3 (去聲)  | (none)                  |
        | 5     | vertical line (a̍) + stop | **se̍k**     | 8 (陽入)  | (none, stop-final)      |
        | 6     | (unmarked) + stop        | **sek**     | 4 (陰入)  | ˋ on stop-final         |

        **Note:** KPPY 調號 follows the 八聲 (eight-tone) framework — only 調號 1 aligns with PFS # 1; the rest diverge (調號 2 = PFS 3, 調號 3 = PFS 4, 調號 4 = PFS 6, 調號 5 = PFS 2, 調號 8 = PFS 5). See `hakfa-roman-orthography-converter` for the full cross-reference.

    *   **Avoid:** repurposing POJ tone numbers (1–8) for Hak-fa data — the diacritic→number mapping differs from POJ (e.g. PFS 1 = circumflex, but POJ 1 = unmarked; PFS 5 = vertical-line stop, but POJ 5 = circumflex), so reusing POJ numbering for Hak-fa silently misencodes tones.

## Why This Matters

Standardizing terminology respects the linguistic identity of Hakfa as a language in its own right, distinguishes the multiple competing Roman Orthographies (which are not interchangeable), and keeps Hak-fa tone numbering aligned with the long-standing 長老教會 PFS tradition rather than borrowing from Taigi POJ.
