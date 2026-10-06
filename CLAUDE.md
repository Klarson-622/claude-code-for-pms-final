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
