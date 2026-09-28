# context-rewrite

A Claude skill for cleaning up "slop" (generic, padded, template-like filler) and fixing context mismatches in drafts such as esai, KTI/LKTI, laporan, proposal, and tugas, in Indonesian or English.

The skill treats the user as the only source of facts. It never invents numbers, sources, or results; anything missing is asked for or marked `[perlu data: ...]`. It has two modes:

- **Mode A — Bersihkan & sesuaikan:** clean an existing draft and align it with the user's purpose, audience, and data.
- **Mode B — Tulis ulang lewat tanya jawab:** rebuild the text section by section from the user's answers to concrete questions.

After either mode, a correction pass (putaran koreksi) fixes only the flagged sentences and shows each change as sebelum → sesudah.

It is not for removing watermarks, disguising AI authorship, or beating AI detectors.

## Install

Copy `SKILL.md` into a folder named `context-rewrite` in your skills directory (for Claude Code, `~/.claude/skills/context-rewrite/SKILL.md`), or upload it as a custom skill in Claude.
