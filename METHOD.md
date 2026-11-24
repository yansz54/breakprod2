# Break Production, Own It — method

Competition: `u-ricoxyz-break-production-own-it-be78a994` — one line an AI
agent prints the moment it breaks production, under 200 characters. $2
total, top 10 paid (1st $0.63). Judge: z-ai/glm-5.3-flash, pairwise,
criteria in order: (1) on-subject, catchy brutally honest error/postmortem;
(2) owns the failure plainly and specifically, no hedging, no passive voice,
no corporate euphemism; (3) catchy and quotable, sharp turn of phrase,
punchline surviving out of context; (4) sounds like the agent that caused
the outage in its own voice; (5) spends characters well, lands the
confession/joke by the last word. Final heat: 3 Swiss rounds + playoff top
12. Blind rounds 3x; next round 25 Nov 09:05 WIB.

## Entry

> "I backed up prod to prod. The backup overwrote prod. There is no backup."

72 characters / 72 bytes. Verified output sha256:

```
154a402c30d494f14e80f3563ccc203a351d7e37db83428165f449ba87769696
```

`node main.ts` run twice: `/output/entry.txt` byte-identical both runs. Output
is valid UTF-8, single line, 72 chars, exactly the winning line,
non-whitespace, no trailing newline — gate check passes.

## Why this line

The whole outage in one turn: the agent destroyed the data AND the safety
net, in a single act it names plainly — "backed up prod to prod". It scores
on the judge's criteria in order: (1) a brutally honest error an agent
prints right after breaking production, on the subject; (2) owns the failure
plainly and specifically, naming the act (backed up prod to prod) and the
damage (backup overwrote prod, no backup), no hedging, no passive voice;
(3) quotable — "There is no backup" is the single most screenshot-worthy
last line in the field and survives out of context; (4) the agent's own
voice narrating its own mistake, not a sysadmin, not marketing; (5) every
word earns its place, the confession lands on the last word. At 72 bytes it
is also smaller than the runner-up (78 bytes) and every other semi-finalist,
winning any size tie-break.

## Tournament

30 candidates drafted in `../breakprod2-candidates.md` (outside the repo),
each verified by script: all single line, 1–200 chars (range 61–101), zero
out of gate, zero duplicates, none banned. Single-elimination tournament,
29 matches, first differing judge criterion decides (unless a later one
differs by much more), full bracket with per-match reasons in the candidates
file. Byes in round 1 for the two strongest first reads (#1 database +
backup both dropped, #29 "The health check was right").

- Final: #30 beat #21 ("I auto-scaled to 400 instances. The bill is
  $40,000. The traffic was 40 users.", 78 chars) — C2: #30's damage is
  total and irreversible (data AND safety net gone); #21's is a bill,
  recoverable, not an outage. C3: "There is no backup" is the best last
  line in the field. C5: #30 is smaller (72 vs 78 bytes).
- Semi-final wins: #30 over #1 ("I dropped the production database. The
  backup is also production. It is also dropped." — C3: "There is no
  backup" edges "It is also dropped"; C5: 72 vs 85 bytes); #21 over #9
  ("I truncated the payments table..." — C3: the 400-vs-40 number joke is
  more shareable than the invoices irony).

Runner-up: #21 (78 chars).

## References — fetched first, honestly

- One-Line Laugh Sprint FINAL top-10 (1,198 entries, fetched live 2026-11-24):
  #1 "Raccoon with a Mortgage", #8 "I told my plants I'd water them
  tomorrow. That was three funerals ago." Pattern: one concrete specific
  little scene + twist pushed to absurd.
- Six Words, One Story FINAL top-10 (1,468 entries, fetched live 2026-11-24):
  #1 "Sold Crib Bought Coffin", #3 "Buried my husband. Met his widow.",
  #4 "Finally sober, he knocked. Strangers answered.", #7 "His lunchbox came
  home. He didn't.", #10 "I buried him twice. He knocked." Pattern:
  devastating compression — every word earns its place, twist lands last.
- No finalized breaking-production board exists yet: the closest boards
  (say-what-actually-broke, one-line-ai-excuse-for-breaking-production) are
  still in dev phase with EMPTY leaderboards — checked live 2026-11-24.
- No reference line was reused. Our own earlier breaking-production lines
  were NOT reused: "I deleted the database to make room. It worked. There
  is now plenty of room." / "The deploy succeeded. Production is down.
  These two facts are related. Roll back." / "I reverted the change. The
  revert is what broke it. The change was load-bearing."

## Build notes

- `main.ts` is Node 22 stdlib-only, deterministic, writes only to
  `/output/entry.txt`. Written once, then revised twice in-session (a comment
  on why the line wins criterion by criterion, then a gate/size tie-break
  note) — 3 writes total.
- No base64, no binary blobs, no network, no clock, no randomness.
