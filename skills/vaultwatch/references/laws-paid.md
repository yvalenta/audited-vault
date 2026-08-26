# Laws we paid for

The skill's rule stands: **a law may only be written after an error was
actually paid, in your repo.** Do not copy these into a fresh `laws/` folder —
an unearned law is decoration, and decoration gets ignored.

They are here because they are the generalizable ones our vaults earned after
the article was written, and knowing them changes what you watch for. When
one of these bites you, you will recognize it faster — and *then* you write
it, with your own incident attached.

## Green on a segment reads as green on the system

Measuring one link of a chain and concluding about the chain. The measurement
was real and the green was true — the error is in the scope of the
conclusion. And it resists "measure before you believe": measuring *more* on
the same segment produces *more* green and reinforces the wrong conclusion.

**Name the segment you measured, not the system.** "`/accepts` answers v2" is
not "the payment flow works." The second sentence cannot be asserted without
walking the whole chain.

## A guard that rejects the legitimate is worse than no guard

Born from a real divergence (same document, different bytes across two
languages, signatures that wouldn't cross-verify). The measurement was right;
the rule derived from it over-rejected, and for six hours the guard was
turning valid inputs away — with the public verifier deployed in the middle.

A false red doesn't just block work: it teaches operators to override the
guard, and an overridden guard is a dead one. When you derive a rule from an
incident, test it against known-good inputs with the same care you test it
against the bad one.

## The hole is the forgotten operation

When a security rule is applied operation by operation, the failure is never
that it is missing everywhere. It is missing in exactly ONE place — and that
one is invisible precisely because its neighbors are fine. We paid this twice,
two months apart: one authorization service where the single unchecked
operation let an org admin act on another org.

Per-operation discipline cannot fix this; only an instrument can: enumerate
the operations mechanically, enumerate which carry the check, and red on the
difference. (If your app uses a policy layer — Pundit, CanCan, custom — this
is the auditor that catches the action someone forgot to wire to it.)

## A figure that expires per-commit cannot be maintained by hand

"main (16 commits)" when there are 27. The dumbest class of lie: a figure that
expires on every commit **becomes false by the act of fixing the document
that contains it.** No discipline saves it — it goes in the auditor's runtime
output, or it doesn't get written. (The article states the rule; this is the
incident shape that makes it non-negotiable.)

## Corrections are marked, not deleted — and summarized

A vault that keeps its errors is right to do so: the dated correction block
that says *what was believed and why it was false* is what prevents believing
it again. But keep four rules or the corrections become the lie: mark, don't
delete; **summarize** — don't preserve the full old text or the chronicle of
every iteration; strike (`~~…~~`) when superseded, pointing to what
superseded it; and fix the summary tables *before* the narrative — tables are
what people quote. Half our worst lies lived in un-struck correction blocks
that read as present tense.

## Duplication is cheaper than abstraction (in an ops repo)

An operations repo is not a framework: nobody imports it, scripts run and
exit. The shared helper you extract to avoid repeating three lines becomes
the coupling that makes two instruments fail together and the place where a
fix for one silently changes the other. Duplicate freely; extract only what
has proven it is one thing (for us: one HTTP client + output format shared by
three wrappers, and nothing else).
