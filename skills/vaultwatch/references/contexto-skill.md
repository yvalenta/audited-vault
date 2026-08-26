# Template: the repo-local cold-start skill

The ritual survives only if a cold session runs it without being told. Ship
it as a skill **inside the repo** (`.claude/skills/<name>/SKILL.md` — we call
ours `contexto`), so any agent that opens the repo cold loads the same doors,
the same gates, and the same refusals. Everything below is the distilled
shape of ours; adapt names and commands, keep the bones.

## Frontmatter

The description must catch both the explicit calls ("load the context", "run
the auditors", "what's the state here") and the implicit ones ("what works?",
"what's broken?", "what's next?") — a cold session rarely knows the skill's
name. State the ending up front: it finishes by answering "ok" with a table.

## Phase 1 — Read, writing nothing

In order, and the order matters — each layer is read for something different:

1. The index (`CLAUDE.md` / vault README) — the map.
2. `HANDOFF.md` — the door, **including the "what can be done now" table:
   the future layer, read BEFORE measuring.** The obvious fix for a red is
   often wrong for where the project is going; if a red later asks for
   something this table contradicts, that contradiction is itself a finding.
3. `state/*.md` — every file the glob finds (never an enumerated list — ours
   aged the day a new state file was born). The figures the auditors compare.
4. `laws/*.md` — all of them; none is optional in the correction phase.
5. The lie autopsy in `history/` (see below) — what *kind* of lies this repo
   produces, so Phase 3 knows what to hunt.

Numbered reference docs load on demand, not up front — loading everything
dilutes what matters. **Note contradictions while reading; fix nothing yet.**
Correcting before measuring is how lies get manufactured.

## Phase 2 — Measure

Two gates, stable even as the repo grows (because the runner discovers by
glob): the no-network gate (coherence + all suites) and the network gate
(world audit + probes). Teach the reader to read the rows the runner prints —
they are the living list; do not hardcode instrument names in the skill.

Include the red-classification table (doc-vs-doc / doc-vs-world / code broke
/ artifact doesn't derive / external invariant), the re-run-once rule for
non-reproducing reds, and the humility banner: an exit 0 proves what the
scripts watch is still in place — nothing more. What smelled wrong in Phase 1
still counts even if everything is green.

## Phase 3 — Correct (documentation only)

The correction rules from the skill body, plus the two locally-learned ones
that recur everywhere: before writing any figure into a note, check it
doesn't latch an existing anchor (cite the assertion site instead of
repeating the number); and when closing an arc, fix the summary tables
before the narrative.

If the correct fix requires touching an instrument: **stop, show the red,
name the change, argue why the demand rises, and ask.** The skill never
edits an auditor on its own authority.

## Phase 4 — Earn the green

Re-run both gates with the fixes in place. Then the negative proof, per
corrected claim: break it by hand, confirm red, restore. Cap of three rounds
— a red that survives three is the world or the instrument; stop and say so.

## Phase 5 — Commit

By tree state: clean → commit yours; dirty-and-green → commit only yours and
list the rest untouched; dirty-and-red → no commit, list and stop. Follow the
repo's commit-message customs. No commit — didn't happen.

## Phase 6 — The earned "ok"

Short. The caller invoked this to start working, not to read a report:

```
ok — context loaded

|  |  |
|---|---|
| Vault      | read: door, map, state/, laws/, lie autopsy |
| No-network | green — N checks, N tests                   |
| Network    | green — probe N/N · world audit N/N         |
| Fixes      | what was false, where fixed, negative proof |
| Commit     | <sha> <subject> — or why there was none     |

Next: the "what can be done now" lines from HANDOFF.
```

Every figure in that table comes from this session's runs — never from
memory, never from the doc. **"ok" only if green.** If something stayed red,
the answer starts with what, the instrument's output, and why it wasn't
fixed. An "ok" over a red is exactly the class of assertion the vault exists
to prevent.

## The No-list

The skill states what it never does, explicitly — an agent that loads context
must know where its mandate ends:

- Never runs anything that **writes to the world** (deploys, publishes,
  signs, pays, POSTs). If context reveals something ready to publish, it says
  so and waits.
- Never fixes code. A red suite is a work session: report and stop.
- Never touches an instrument without asking — even when the fix is correct
  and written down.
- Never deletes worktrees or anything else; abandoned copies are reported.
- Never invents a figure. Every number written came from a run this session
  made.
- Doesn't do the work the HANDOFF table enumerates — it reads it to avoid
  contradicting it, and to say what's next.

## One more file worth having

The lie autopsy: a `history/` note that classifies the false claims your
vault has produced (ours: "rounds of lies", by class and count). It is the
highest-yield read for a cold session — you cannot hunt what you cannot
name — and it keeps the humility banner honest: the count is real, so the
green never gets worshipped.
