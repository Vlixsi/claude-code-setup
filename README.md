# claude-code-setup

A small, tested setup for Claude Code memory that stays usable as it grows.

**Why:** Anthropic's engineering post on agent memory (Nov 6, 2026) notes that Claude Code's auto memory loads only the first **200 lines or 25 KB** of `MEMORY.md` at the start of a session. Anything past that is not loaded at startup.

So instead of one long memory file, this setup uses:

- **one short index** (`MEMORY.md`) that always fits under the limit
- **one file per topic**, opened only when it's needed
- **a rule to cite the file** every answer came from

## Install in 5 minutes

1. Copy `CLAUDE.md` into the root of your project (or merge it with yours).
2. Look at `memory/MEMORY.md` as the template for your index. Keep it short: one line per topic, a pointer, and when to open it.
3. Put details into topic files like `memory/decisions.md` and `memory/lessons.md`.
4. Open Claude Code in your project and paste the prompt from `prompts/reorganize-memory.md`. It shows a plan first and changes nothing until you approve.

## Structure

```
claude-code-setup/
├── CLAUDE.md                     # project rules, including the memory rules
├── memory/
│   ├── MEMORY.md                 # the short index (stay under 200 lines)
│   ├── decisions.md              # example topic file
│   └── lessons.md                # example topic file
└── prompts/
    └── reorganize-memory.md      # paste into Claude Code to restructure your memory
```

## Rules of thumb

- The index holds **pointers, not facts**.
- One topic per file, named after what's inside (`clients-acme.md`, not `notes-12.md`).
- Long lines count toward the 25 KB cap, so keep index lines short.
- Every so often, merge duplicate topics and delete stale ones.
- If something isn't in memory, Claude should say so instead of guessing.

## Source

- Anthropic Engineering, "The components of agent memory" (Nov 6, 2026)

Made by [@Vlixsi](https://x.com/Vlixsi). MIT licensed.
