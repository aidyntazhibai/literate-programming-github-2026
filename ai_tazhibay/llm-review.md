# LLM review of spec.md

## Setup

- LLM: Claude Opus 5.5 (`claude-opus-5-5`) in Claude Code (desktop app), default effort.
- Prompt: `Review spec.md`
- Strikethrough marks output that I judged incorrect or irrelevant.

## Review history

| Round | Findings | Main changes made |
|---|---|---|
| 1 | 7 | Examples 10–11 written as exact lists; named `str.lower()` (not `casefold()`) with a `ß` example; added a Kazakh capital-letter example; removed the locale sentence. |
| 2 | 5 | Example 9 written with `\u` escapes instead of an invisible combining mark; named the file `top_words.py`; renumbered the examples; added an example for U+02BC. |
| 3 | 1 | None needed (the last review, below). |

## Output of the last review (round 3)

I checked all 18 examples by hand against the algorithm: steps 1–5 give each expected output, including the code point orders the examples rely on (`с` U+0441 < `қ` U+049B, `е` U+0435 < `ё` U+0451, `'` U+0027 < `ʼ` U+02BC, `s` U+0073 < `ß` U+00DF). The interface, the definitions, and the algorithm agree with each other, and the five steps determine one result for every input, so two implementations that follow the spec cannot return different lists.

**Must fix:** none.

**Should fix:** none.

**Minor**

1. ~~Step 1: `str.lower()` turns the Turkish capital `İ` (U+0130) into two characters, `i` + U+0307. The spec defines this result, but no example shows it. Add an example such as `"İstanbul"` → `[('i̇stanbul', 1)]`.~~

## My notes on the struck-out item

- 1: Rule 1 already defines the result exactly, so the item does not affect correctness. Turkish is not one of the three languages the spec targets (English, Russian, Kazakh), so an extra example would only make the spec longer.
