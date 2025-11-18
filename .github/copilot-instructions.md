## Quick overview

This repository contains short Python exercise scripts used in a class context. The current files are simple, top-level scripts (no packages or test harness). The main focus is bitwise operations and small console I/O.

Key files to inspect:
- `activity 1.py` — counts ones/zeros in the binary representation of an integer (uses `input()` and `print`).
- `activity 2.py` — intends to check whether a specific bit is set; this file contains pseudocode and has syntax errors (see examples below).

Repository facts that matter to agent edits
- These are standalone scripts (run with `python "activity 2.py"`). Filenames include spaces — preserve quoting or rename carefully and update any references.
- No dependency manifest (requirements.txt/pyproject.toml). Assume standard Python 3. Use small, local changes only unless the user asks to restructure.
- No tests present. Before changing behavior, run a quick syntax check (see suggestions) and prefer minimal refactors that keep the console I/O-based contract.

What to do when editing code here (concise rules for an AI coding agent)
1. Preserve top-level console contract: functions read integers via `input()` and print outputs. If you refactor to functions, keep a small runner that maintains the same prompts.
2. Fix obvious syntax/pseudocode issues but keep the original intent. Example: `activity 2.py` contains literal pseudocode lines like `check if (n AND mask) equals 1 or 0` and malformed `else print(...)` — replace these with a small, explicit implementation (use `mask = 1 << (n-1)` and `if number & mask:` then print `f"bit {n} SET"` else `f"bit {n} NOT SET"`).
3. Use defensive input handling only when explicitly asked; avoid changing user-visible prompts or removing `input()` unless instructed.
4. When renaming files to remove spaces, update any local documentation and show the rename in a single commit; include both old and new names in commit message so students can find it.

Quick checks to run locally (PowerShell examples)
- Syntax check: `python -m py_compile "activity 2.py"` — fails if syntax errors remain.
- Run a script: `python "activity 1.py"` or `python "activity 2.py"` (quotes required because filenames contain spaces).

Patterns and examples discovered in code
- Console-based exercises: inputs are converted with `int(input(...))`; expect ValueError on non-integers. Example: `number=int(input("Enter a number:"))` in `activity 1.py`.
- Bitwise intent: both files use bit operations — `n & 1`, shifts (`>>=1` or `1 << (n-1)`) and masks are the right primitives.

Edge cases and hints for fixes (documented, not enforced)
- `activity 1.py` currently mixes logic and printing inside the loop; if you simplify logic, keep the visible output similar for students.
- `activity 2.py` needs correction for indentation, removal of pseudocode lines, and correct print formatting (escape sequences like `n\SET` appear accidental).

When to add tests or refactor
- Ask the user before introducing unit tests or changing the UI to a function-based API. If asked, add a small `tests/test_activity2.py` that imports a newly-extracted pure function and verifies behavior for a few bit positions.

If you need clarification
- Ask whether keeping exact prompt text is required (students may rely on it), and whether filenames may be normalized (remove spaces). Also ask whether you should auto-fix non-functional issues (PEP8) or only correctness bugs.

Contact / follow-up
- After making edits: run `python -m py_compile` and share results. When proposing a refactor (e.g., move logic into functions), include a one-paragraph rationale and a short migration plan so instructors can accept or reject it.

— End of copilot instructions —
