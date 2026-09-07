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

## The auditor that counts is a claim about the world too — check its unit

Our token auditor summed every line of the transcript log. An assistant
message is written to that log as two or three lines (thinking, text, tool
call) that repeat the same usage block, so every total was inflated **2.59x**:
20.2 billion tokens a month where 9.0 billion had been spent. It served
percentages honestly for weeks — the ratios survive a constant factor — and
nobody audited the totals *because it was the auditor*.

**An instrument's unit is an assertion like any other; dedupe by the source's
own identity (here, the message id) and write the unit next to the figure.**
When two instruments disagree by a constant factor, the factor is the finding,
not the noise.

## The measuring agent names its model — inheriting is a decision too

A twelve-agent measurement run, launched without a model per agent, put
eleven of them on the frontier model: grep over logs, timing a hook, three
curls. The month said the same at scale: 828 subagents, 70% of their tokens
on the largest model, 4.9% on the mid one, 0% on the small one. And a trap
we only found by reading the binary: in Claude Code 2.1.260 the built-in
read-only `Explore` agent inherits with a *cap* that resolves to Opus when
the session runs a model outside its list — the cheap explorer was the
expensive one.

**Every launch names its model, explicitly, by the class of work:** the
small model runs commands and returns the tape; the mid one reads,
classifies, summarizes and drafts; the frontier model is reserved for
refutation and for the judgments the ritual exists not to delegate — that is
the instrument that paid rent, and stepping it down is changing the unit. If
the small one fails for capacity, go up one step and write it down; never
start at the top "just in case".

## Delegation is not free — delegate by size, not by class

A launch of the read-only explorer cost ~2.6 million tokens, about eight
turns of the parent session; a general agent ~8.4 million, about twenty-six.
The three days with the most delegation were the three days the subscription
hit its limits five times. Handing a loose `grep` to an agent does not save
the parent anything: it pays the agent's cold start on top of its own turn.

**Launch an agent only when it replaces at least ~8 reads or when the output
it would drag into the parent exceeds ~3k characters** — a suite's tape, a
log, a sweep across files. Below that, the parent does it. The cold-start
ritual's *measure* phase is the canonical case that clears the bar.

## The repeated call is a protocol defect, not a model defect

4,004 identical calls repeated three or more times in a month — the champion
a browser screenshot taken 170 times by 15 agents re-capturing a screen that
had not changed: 11.6% of the month's spend for 268 output tokens a turn.
Moving that loop to a cheaper agent changes who pays for the loop, not the
loop; the agent cannot tell that nothing changed.

**Make sameness visible mechanically.** A post-tool hook that hashes the call,
counts consecutive identical ones and, at the third, tells the agent the
screen did not change and to change action — read the page, declare what it
expects to see — costs 0.08 s a call and needs no model. Fix the protocol
where the repetition happens, not the model that repeats.

## Past the cut, the session closes — it does not resume

Measured on a month of sessions: 86–88% of the spend happened in turns whose
context was already above 200k, where every token of output cost 2–7x what
it had cost earlier in the same session (burn 244x–680x against 98x–139x
below). Long sessions do not degrade gracefully; they get expensive first and
confused second.

**A session that crosses the cut closes the task it holds — state and log in
the task file, what is missing written for a cold session to pick up — and
stops.** The next session starts fresh from the task. A session past the cut
is never resumed or forked: that drags the whole context along. The ritual
is what makes the cut cheap: the handoff is a commit, not a conversation.
