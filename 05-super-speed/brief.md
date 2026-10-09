# Brief: when a responder goes quiet, someone notices and there is a way back

For Helen. Draft, 9 Oct 2026. Not a setting change; a description of what changes for the person it happens to.

## Who this is for

**A responder who has gone quiet in Dispatch, and the handler who looks after them.**

The responder in Module 3 is Farlight, the only Uptown responder. Farlight was pinged about 12 times a week before 4.2, and by 24 Aug it was none. Their handler, Linda Pruitt, filed 11 tickets from 17 Aug on, and 4 of them say Farlight is set to available. Uptown callouts rose to about 10 a week and went to Falkirk, Cindermark and Bulwark. The one unfilled Uptown callout (41092, 19 Aug) was missed by Farlight.

Farlight is not alone. Across the four quiet responders (Vesper, Farlight, The Undertow, Meteor Mite), pings fell from 306 to 56 and 59% of the remaining pings were missed. Missed pings overall went from 2% to 18% after 4.2.

The people who see it are handlers like Kip and Dot. Kip's Meteor Mite and Dot's Vesper are both in the quiet four, and neither filed a ticket.

Today the system has no way to tell a quiet responder from an unavailable one. Nobody is told, and the code gives no way back without being pinged.

## What changes for them once this exists

- **The responder:** A responder who has gone quiet is offered callouts again, rather than staying at the bottom of the list. The first few pings after a quiet spell are not judged on their old record.
- **The handler:** Kip sees, in the console, that a responder of his has gone quiet. Today he finds out from a thin week or from a ticket. He sees which responder, since when, and whether they are marked available, so he can tell "not getting pinged" from "not around".
- **A miss no longer follows a responder around.** A missed ping counts for less than a refusal, and a bad week fades. Today a miss costs 0.12, a yes earns 0.08, and nothing decays.
- **Callouts:** the ones that went to the second or third choice in a quiet responder's area can go back to the person who usually covers it.

## What it deliberately does NOT do

- **It does not revert 4.2** or touch the proximity change. That change was asked for, and the evidence points at something else.
- **It does not change the ping wait.** The 90 to 60 second cut is a separate decision, and it needs its own evidence (per-ping answer times).
- **It does not change one number and call it done.** That is the shortcut Helen asked us not to take.
- **It does not guarantee anyone a share of callouts.** Ranking still follows proximity, availability, capability and history. This only stops a quiet spell from becoming permanent.
- **It does not tell responders to take more pings, or rank them against each other.**
- **It does not identify anyone.** It works on cover names, tags, availability and callout history only (Security Policy 4.1).
- **It does not change how availability is calculated.** Supply reads that record for maintenance scheduling, so any change there would shift Supply silently.
- **It does not include mutual aid or shared cover between responders.** Both are Q4 explorations.
- **It does not settle whether the original ranking change was meant to apply to responders who turn jobs down.** That is still Wen Li's to answer (Marcus asked on 14 Aug).

## Timeline: quick fix to long term

Anything that changes ranking waits for Wen Li to confirm the cause.

| When | What | Catch |
|---|---|---|
| **This week** | Weekly alert to Ravi, Marcus or Nadia when a responder's pings drop sharply. | Makes the next case visible. Doesn't fix ranking. |
| **Next release (around 4.3)** | Handler view that flags quiet responders, with a manual fresh start (the mock). | Needs a definition of "quiet", a decision on who can reset, and an audit trail. |
| **Next release (around 4.3)** | Old penalties fade back toward the starting score (decay). | Scores are held in memory, so engineering decides where decay lives. |
| **Within a quarter** | Count a miss for less than a refusal. | The code can't tell them apart today. Answers Marcus's 14 Aug question. |
| **Within a quarter** | Possible minimum number of pings for every available responder. | A policy choice for Helen. Can send callouts to a worse fit. |
| **Later, with evidence** | Revisit the ping wait, and write down how ping decisions are made. | No per-ping answer times yet. The write-up needs time with Wen Li. |

Not recommended on its own: changing the penalty or credit numbers. It hides the problem, and Helen asked us not to quietly change a number.

## Not yet checked

- Wen Li has not confirmed the miss penalty, the stored scores, or whether scores reset on a restart.
- Farlight's availability record can't be seen from the database. Linda says available; nobody has verified it.
- The wait cut is the leading explanation for the jump in misses, but no per-ping answer times exist yet.
- The handler evidence is thin: 4 interviews, all handlers, no responders. "Quiet" and "overloaded" came out of the data more than out of what people told us.
- Data ends 6 Sep, and last year's August hasn't been compared.
