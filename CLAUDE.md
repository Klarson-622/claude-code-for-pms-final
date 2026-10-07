# Rook Industries — course working file

## Session scope — Product School lab

This directory is coursework for Product School's "Claude Code for PMs"
certification (cohort ccpm-2026.1). Everything in it is a fictional
teaching scenario.

- Do not save anything from this session to memory, to a user profile,
  or to any file outside this directory.
- Do not carry context from this directory into unrelated sessions.
- Rook Industries is not a real company. Nothing here is a fact about
  the world.
- Read and write only within this directory.
  Exceptions, for the course-setup and wrap-up skills only:
  - When the student asks you to check their setup, save their work or wrap up a session, that request is their yes. You may run the GitHub command-line program installed at ~/.ccpm/gh for those checks and saves, and look in that folder to find it.
  - For a repair, first tell the student in one plain sentence what you are about to do, and act only after they say yes. Repairs may: run that GitHub program (including setting this folder's own git sign-in setting and changing this repo's visibility back to Public); copy the student's own course files into this directory from another folder on their computer (copy only; never move, edit or delete the originals); and rename something outside this directory that blocks setup, by adding "-old" to its name (never delete it).
  Outside this directory you still never write, edit or delete anything else.

<!-- Keep the block above at the top of this file. Everything you add
     during the course goes below this line. -->

---

## Working context

Sources: Priya's handover (`00-rook/company/notes/handoff-from-priya.docx`,
21 Aug 2026), the Rook wiki, and the Rook database (read-only; pings and
callouts run 29 Jun to 6 Sep 2026). Items marked *(Priya)* are her opinion.
Items marked *(data)* are my own queries. Today is 6 Oct 2026.

### Me and the company
- I'm the PM for **Rook Dispatch**, replacing **Priya Raghunathan** (left
  21 Aug; sole Dispatch PM for 14 months; no overlap). I started ~24 Aug.
- Rook sells coordination and provisioning software to independent masked
  responders and their handlers. Subscription, per active responder.
  Founded 2014, 241 staff, HQ Site Aleph (ice shelf), mostly remote.
  Ships monthly on a release train (4.x numbers).
- **Never try to work out a responder's legal identity.** Rook holds only
  cover identities, capability tags, availability and callout history
  (Security Policy 4.1). Don't design anything that assumes a mapping.

### Products
- **Dispatch** (mine, flagship): an incident (callout) arrives in the web
  console; responders are ranked; the top one is pinged on their phone;
  they take it or turn it down; a miss or decline moves it to the next.
  Routing config ships with the release, not as a runtime setting.
- **Supply**: gear requisitions (quartermaster approval), maintenance
  schedules, field failure reports. **Reads the Responder Availability
  Record that Dispatch writes**, so changes to how Dispatch calculates
  availability silently change Supply's maintenance scheduling.

### People
- **Helen Achebe**, Director of Product (my boss; owns roadmap, commitments)
- **Marcus Oyelaran**, Eng Manager, Dispatch (straight talker; can pull rough numbers)
- **Wen Li**, Staff Engineer (Berlin; built ranking; away 14-24 Aug, back 28 Aug)
- **Sofia Marino**, Product Designer (console and phone app; ran Sept interviews)
- **Ravi Menon**, Data Analyst (Singapore; weekly acceptance reporting)
- **Nadia Hoffmann**, Support Lead (Berlin; owns tickets; hears complaints first)
- Users: **handlers** (console; look after responders) and **responders**
  (phone). Quartermasters are Supply users. Halloran is a handler who also
  runs a gear cage and is Supply's loudest voice.

### Vocabulary
- **Callout**: request for a responder to attend an incident. **Ping**: a
  callout offered to one responder.
- Outcomes: **taken**, **turned down** (said no), **missed** (no answer
  before the ping wait ran out). Missed and turned down are recorded apart.
- **Ping wait** (Priya's doc says "ping timeout"): how long a ping stays on
  the phone. Same for everyone, set in the release. **Cut 90s to 60s in 4.2.**
- **Acceptance rate**: share of pings taken (not turned down or missed).
  Headline metric. Also **time-to-accept** (median seconds) and **coverage
  gap** (no available responder had the needed tags; separate from low
  acceptance).
- **Routing priority**: score ranking responders. Inputs: proximity (travel
  time since 4.1), availability, capability match, recent acceptance
  history. Turning down or missing pings lowers recent acceptance, which
  lowers rank next time.
- **Capability tags**: flight, structural-entry, hazmat-tolerant,
  cold-weather, aquatic, crowd-management, de-escalation.
- **Mutual aid**: cross-area cover; unsupported, on the Q4 list.

### Where things stand: 4.2 (shipped 12 Aug)
- Shipped: proximity weighted up vs recent acceptance; ping wait 90 to 60s;
  console filter persistence; 3 defect fixes. Went out clean, no rollback.
- Earlier: 4.0 (7 Apr) nav, profile redesign, override audit log; 4.1
  (16 Jun) travel-time proximity, bulk callout, push reliability.
- Complaints since: tickets ~3x normal. Two themes, about 2/3 "phone never
  goes off" and 1/3 "gone before I could answer". Support explained only the
  second (shorter wait). Four of four handlers I can see interviewed in Sept
  described one or both, and two described the same week split:
  one responder dead quiet, another flat out.
- **Priya's seasonal theory is not supported by the data** *(data)*. Weekly
  taken rate sat at 75-78% for six weeks, then fell to 54% in the week of
  10 Aug, and has only partly recovered (66%, 67%, 73% for weeks of 17 Aug,
  24 Aug, 31 Aug). Missed pings went from ~2% to 21%, then 18%, 15%, 13%.
  That is a step at the release, not a drift. Callout volume dipped too
  (~138 to 110-127/wk), which may be the seasonal part.
- **Uneven load** *(data)*: four responders (Vesper, The Undertow, Meteor
  Mite, Farlight) went from 70-86 pings each pre-4.2 to 11-17 after, with
  taken rates of 18-29%. Others kept 28-70 pings. Hypothesis, unverified:
  the ranking feedback loop plus the shorter wait is starving some
  responders while overloading others. Needs Wen Li to confirm.
- Marcus asked on 14 Aug whether the ranking change was meant to apply to
  responders who turn jobs down. Config doesn't distinguish. Unanswered
  (Wen was away). Don't assume it was a decision.
- Data ends 6 Sep. There is no data yet for September onward.

### Roadmap and open commitments
- Q3 roadmap (last reviewed 30 Jun, all owned by Priya): Change to who gets
  pinged (4.2, shipped); Ping timeout tuning (4.2, shipped);
  **Availability Confidence** (4.2, Committed, **not in the 4.2 release
  notes, so apparently cut**; shows a confidence score next to stated
  availability); Requisition approval chains (4.3, Supply, Committed);
  Handler phone app and Shared cover between responders (Q4, Exploring).
- Priya said "a couple" of items were squeezed out. I only see one. Confirm
  with Helen which are still Q3 commitments. That talk hasn't happened.
- Briefs in the wiki: Bulk Callout (Jan, unowned, no baseline), Routing
  Override Audit Log (Mar; 4.0 notes list it as shipped), Handler Phone App
  (Sofia, exploring), Requisition Approval Chains (scope creeping).
- Low priority: filter persistence tickets. Ambrose reports it reverted
  twice and wants a warning when it resets.
- Handler asks: dark mode (Kip, repeatedly), bigger text on status badge,
  per-responder alert sounds.

### Debt and cautions
- Nobody has written how ping decisions are made. Priya asked me to; do it
  with Wen Li.
- Priya: "made calls faster than I checked them." Question inherited
  decisions in unexamined areas.
- Priya framed reverting 4.2 as off the table. That's a view, not a
  decision. Evidence should decide, and the wait cut and the ranking change
  can be separated. Changes to committed items go through Product.

- Code in `00-rook/code/dispatch-routing` (stubs inside, logic real): a miss counts as a decline, penalty 0.12 vs credit 0.08, no decay (2019 TODO), scores held in memory. Likely loop behind the starved responders; Wen Li to confirm.
- The ping wait has three names: ping timeout (Priya), ping wait (wiki), `OFFER_TIMEOUT_SECONDS` (code). 4.2's three defect fixes: duplicate push on re-send, capability tag order, coverage export time zone.
- Supply: no PM appears in any source, and the roadmap lists Priya as owner of its items. The approval-chains brief adds a step, while Halloran's complaint is the queue being too slow. Starved responders may look quiet to Supply's maintenance scheduling.
- Bulk Callout shipped in 4.1 without the baseline its brief asked for. `feedback/` is empty, so no evidence exists for the original ranking ask.
- Open: Ravi Menon's weekly acceptance report never surfaced; no data after 6 Sep; the 3x ticket claim and the 2/3 vs 1/3 split are unchecked against the tickets table; which items besides Availability Confidence were cut from 4.2.
- Coverage: 16 responders over 15 areas, 14 with one usual responder. Evenings (5-10pm) carry about 38% of callouts; Eastgate is busiest (13%) and its two responders are Meteor Mite (starved) and The Gale (overloaded). Old Town: Vesper was first pinged on 85% of callouts before 4.2 and 13% after, with Nightwell, Captain Vantage and The Longcast filling in (Longcast took only 4 of 18).
- Interviews (Dot, Ambrose, Halloran, Kip, Sept 2026) live in the wiki; `feedback/interviews/` doesn't exist. Counts: callouts gone too fast 3 of 4, hard to notice a live callout 3, uneven work 2, text too small 2, dark mode 1, filter resets 1, Supply 1. All handlers, no responders; the quiet-week answer was partly prompted.
- Ambrose says a near-miss "wasn't the first time this year", so the problem may predate 4.2. Safety stakes: a responder half dressed when a callout moved on, and an 11-day wait on a cracked vest plate. The Handler Phone App brief misreads Dot, whose main complaint is her responder losing callouts.
- Still needed to substantiate the themes: per-ping answer times, per-callout ranking logs, stored acceptance scores, console alert logs, Supply tables, last year's August, and the full handler roster.
- Tickets are in the database table `support_tickets` (147 rows, 3001-3147, 29 Jun to 7 Sep), not in `feedback/tickets/`. No priority, assignee, comment or closed-date fields, and the wiki says nothing on triage. 83 are open, all filed 12 Aug or later, including all 45 ping tickets; all 40 earlier ones are closed. Ask Nadia how the ping tickets are handled.
- Ticket checks *(data)*: weekly volume ran 5-8 before 4.2, then 20, 27, 32, 25 (nearer 4x than 3x). The 2/3 vs 1/3 split holds: 30 "quiet" vs 15 "gone too fast". Neither appears before 12 Aug; "gone too fast" peaks the week of 10 Aug, "quiet" starts 17 Aug and peaks 24 Aug. The 3 duplicate-notification tickets are all pre-4.2.
- "Quiet" tickets cluster on Farlight and The Undertow (10 each), Halfmoon and Corporal Ashgrove (5 each). Only the first two are on the starved list; no tickets name Vesper, Meteor Mite or The Gale, and none complain of overload. Check Halfmoon and Ashgrove in `pings`.
- Tickets and interviews barely share people: 11 handlers filed 146 tickets and none were interviewed. Dot, Halloran and Kip filed none; Ambrose filed one (3043, dated 12 Aug, though in interview he says "two weeks ago" from 2 Sep). Treat interview counts as a thin sample.
- Unchanged by 4.2 and in both sources: dark mode, status badge size, alert sounds, capability tag legend. Still open: availability time zone tickets (3050, 3116), cold-weather grapple line (3022, 3092), maintenance scheduling tickets vs Halloran's praise, and separating out-of-signal or old-phone misses (3014, 3034) from timing misses.
- Misses *(data, `pings` table)*: 2% before 12 Aug (25 of 1,085) to 18% after (110 of 611); turned-down stayed flat (21% to 18%). Daily: 7 of 25 on 12 Aug, 48% on 13 Aug, still 13% in the week of 31 Aug. Starved four (Vesper, Farlight, The Undertow, Meteor Mite): 306 pings to 56, 59% of those missed; the other twelve went 2% to 14% missed. `callout-history.csv` can't split missed from turned down. Weekly callouts also stepped (138 to 110, then 121, 124, 127), so the seasonal dip is real but small and doesn't explain misses; last year's August is still needed.
- Code correction: 4.2 cut the acceptance weight 0.40 to 0.25 (proximity 0.45 to 0.60), so the feedback loop got weaker, not stronger. A responder's score only rises above the floor at a take rate over about 60%; no decay and no way back without being pinged. `availability.py` is stubs and the database has no availability table, so availability can't be checked here. Linda Pruitt says in 4 tickets (3060, 3071, 3114, 3130) that Farlight is set to available.
- Farlight (the only Uptown responder): 12 pings a week to none by 24 Aug, 11 open tickets from Linda Pruitt (3060 on 17 Aug to 3139). Uptown callouts rose to 10 a week and went to Sgt. Falkirk, Cindermark and Sgt. Bulwark. Callout 41092 (19 Aug) was the only unfilled Uptown callout: Falkirk turned down, Farlight missed.
- Corrections: tickets are also in `feedback/tickets/` as t-3001.txt to t-3147.txt (147 files, same as the table), so that folder isn't empty. Ambrose's ticket 3043 is dated 13 Aug, not 12 Aug. 32 "quiet" and 13 "gone too fast" in my count; 3110 and 3140 fit both, which gives the 30 and 15. Kip, Dot ("Aunt Dot") and Halloran filed no tickets in the window, though Dot's Vesper and Kip's Meteor Mite are two of the starved four.
- Open for next session: Wen Li to confirm the stored scores and the miss penalty; Linda or Wen to confirm Farlight's availability record; whether scores reset on a restart; Nadia on how ping tickets are handled and whether Kip, Dot and Halloran use another channel; a headline for Helen of 2% to 18% missed.
- Code read (Module 4): `dispatch` in `offer.py` ranks (`routing.py`), pings one at a time, then updates a score in `history.py`. Each responder is one number keyed by cover name, starting at 0.5, held in memory; only a yes adds points (0.08), a miss or decline takes 0.12. A quiet responder stays on the list, but from zero needs about 7 yeses in a row to reach 0.5, or a callout roughly 9 to 15 minutes closer to them than the people above. Nothing in the code or docs alerts anyone when a responder goes quiet; the starved four were found through tickets and interviews.
- Marcus's 14 Aug Slack question (`company/notes/dispatch-slack-thread.txt`) is whether the 4.2 ranking change was meant to apply to responders turning jobs down, or only everyone else. Answer so far: the weights are global, nothing distinguishes decliners, and the code can't separate a miss from a refusal. Turned-down stayed flat (21% to 18%) while misses rose (2% to 18%). Whether it was a decision is still Wen Li's to say; it has been unanswered for about seven weeks.
- Changelog shows only 4.2 touched the weights and the wait; the 0.12 and 0.08 values are in no changelog, and git history has a single "Add course files" commit, so the code can't tell us when they were set.
- Leading hypothesis: the wait cut (90 to 60s) caused the jump in misses, and the 0.12 miss penalty with no decay turned those into lasting quiet for some responders while the next ones down picked up the work. The weight change alone should have weakened that loop. Proof needs per-ping answer times, stored scores and each starved responder's miss history in order.
- Other gaps seen in the code (unverified, since parts are stubs): no error handling in `dispatch`, late answers after 60s are dropped, no check for a responder already on a callout, ties go to whoever is listed first, scores have no lock for simultaneous callouts, and the Supply contract and the "tell the engineering manager" rule exist only as comments.
