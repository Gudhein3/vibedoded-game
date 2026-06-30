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
   - Parenthesize conditions in `if` / `while` expressions.
   - Example (preferred):
     - `if (a < b) x; else y;`

2. **Signed integers are not supported (current compiler behavior)**
   - Do not rely on signed comparisons for negative checks.
   - To test negativity, use sign-bit checks:
     - `(x & 0x8000000000000000) != 0`
   - Prefer helper procedures like `is_neg(x)` and `neg(x)`.

3. **Expression-style functions**
   - Keep SB expression conventions (`fn(args)! expr;` or block-expression form) intact.
   - Avoid introducing syntax not accepted by current `sbc`.

4. **Character/input handling**
   - Prefer explicit integer keycodes when needed (e.g., `87` for `W`) to avoid parser/runtime ambiguity.

5. **Hex literal/style compatibility**
   - Avoid risky literal styles when parser compatibility is uncertain.
   - Decimal masks/constants are acceptable and often safer.

6. **Formatting requirement**
   - Files committed by agents must preserve normal newline formatting.
   - Do not commit minified/one-line source blobs unless explicitly requested.

## Collaboration notes

- Human maintainer decisions override this file.
- If a requested change conflicts with these notes, ask for clarification or document the exception in the commit message.
