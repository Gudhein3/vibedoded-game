# AGENTS.md

This repository permits AI-assisted commits.

## Commit attribution policy

- All commits authored by an LLM agent MUST start with this exact prefix in the commit title:
  - `[LLM] `
- Example:
  - `[LLM] Fix movement handling in main.sb`

## Language notes for SB (`sbc`)

These notes are mandatory guardrails for edits in this repository.

1. **Condition parsing**
   - Parenthesize conditions in `if` / `while` / `for` expressions when expressions may be ambigous and don't when they aren't.
   - Example (preferred):
     - Forbidden `if neg(a) -a; else a;` (Here's an ambiguity with `neg(a)-a`, which may be interpretted as `(if (- (neg a) a))` instead of `(if (neg a) (- a))`)
       Prefer    `if neg(a) {-a}; else a;`
     - Forbidden `if (a < b) x else y;` (Here's no ambiguity with interpretation `a < b x`)
       Prefer    `if a < b x; else y;`

2. **Signed integers are not supported (current compiler behavior)**
   - Do not rely on signed comparisons for negative checks.
   - To test negativity, use sign-bit checks:
     - `(x & 0x8000000000000000) != 0`
   - Prefer helper procedures like `is_neg(x)` and `neg(x)`.

3. **Expression-style functions**
   - Keep SB expression conventions (`fn(args)! expr;` or block-expression form) intact.
   - Avoid introducing syntax not accepted by current `sbc`.

4. **Character/input handling**
   - Prefer character literal syntax (`'W'`) instead of integers (`86`) when specifying a character

5. **Hex literal/style compatibility**
   - Hex literals are allowed

6. **Formatting requirement**
   - Files committed by agents must preserve normal newline formatting.
   - Do not commit minified/one-line source blobs unless explicitly requested.
   - Lines must be 4 space indented

7. **Use syntax features of SBC**
   - Examples can be finded at [examples-for-ai.sb](./examples-for-ai.sb)

## Collaboration notes

- Human maintainer decisions override this file.
- If a requested change conflicts with these notes, ask for clarification or document the exception in the commit message.
