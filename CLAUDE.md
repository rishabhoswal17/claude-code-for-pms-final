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
- Answer only the question the student asks, from the sources they
  name. Don't investigate beyond it or offer a theory about what
  Release 4.2 changed unless they ask for one.
- Read and write only within this directory.
  Exceptions, for the course-setup and wrap-up skills only:
  - When the student asks you to check their setup, save their work or wrap up a session, that request is their yes. You may run the GitHub command-line program installed at ~/.ccpm/gh for those checks and saves, and look in that folder to find it.
  - For a repair, first tell the student in one plain sentence what you are about to do, and act only after they say yes. Repairs may: run that GitHub program (including setting this folder's own git sign-in setting and changing this repo's visibility back to Public); copy the student's own course files into this directory from another folder on their computer (copy only; never move, edit or delete the originals); and rename something outside this directory that blocks setup, by adding "-old" to its name (never delete it).
  Outside this directory you still never write, edit or delete anything else.

<!-- Keep the block above at the top of this file. Everything you add
     during the course goes below this line. -->

---

## Working context

Sources: rook-wiki (About Rook, Glossary, Team directory, Releases, Q3
roadmap, Product briefs, 4.2 page comments) and
`00-rook/company/notes/handoff-from-priya.docx`. Read October 2026.

### My role
I'm the new PM for **Rook Dispatch**. I took over from Priya Raghunathan,
who left on 21 Aug 2026 before we overlapped. Her handoff doc is all the
handover I got. My director is Helen Achebe.

### The company and products
- Rook Industries sells coordination software to independent masked
  responders and the handlers and quartermasters who support them. To the
  public it presents as a logistics and workforce-coordination vendor.
  Revenue is a subscription per active responder. HQ is Site Aleph; there
  are offices in Berlin, Singapore and Cornwall. Most staff work remotely.
- **Rook Dispatch** (mine, the flagship): ranks available responders for a
  callout, pings them on their phones, and records whether they take it.
  Handlers use the desktop console; responders use the phone app.
- **Rook Supply**: requisitions, maintenance and field failure reports, for
  handlers and quartermasters. It reads Dispatch's Responder Availability
  Record.
- Monthly release train, numbered 4.x.
- **Hard rule:** we never store or work out a responder's legal identity.
  This is contractual (Security Policy 4.1). Never design or analyze
  anything that assumes we know who a responder is.

### People (Dispatch team; 4.2 comments are signed by role)
| Role in comments | Name | Location | Notes |
|---|---|---|---|
| Engineering manager | Marcus Oyelaran | Site Aleph | Runs Dispatch eng. Priya: "start here." |
| Staff engineer | Wen Li | Berlin | Built the routing (who gets pinged). Only real source on it, since there's no doc. |
| Product designer | Sofia Marino | Site Aleph | Console and phone app. Ran the September interviews. |
| Support lead | Nadia Hoffmann | Berlin | Owns tickets and hears about handler pain first. Priya suggested a standing 15 min. |
| Data analyst | Ravi Menon | Singapore | Owns the official weekly acceptance-rate numbers. |
| Director of Product | Helen Achebe | Site Aleph | My director. Owns roadmap and commitments. |
| (former PM) | Priya Raghunathan | — | Left 21 Aug. Marcus has her number. |

Customer names that come up: Halloran (Supply-side handler, keeps the
gear-cage spreadsheet) and Aunt Dot (handler, interviewed in September).

### Vocabulary that matters
- **Callout** is a job. A **ping** is one callout offered to one responder.
  The outcome is **taken**, **turned down** or **missed** (no answer before
  the **ping wait** ran out). Turned down and missed both pass the callout
  to the next responder.
- **Acceptance rate**: the share of pings taken. This is the headline metric.
  **Time-to-accept**: median seconds from ping to taken.
- **Coverage gap**: no available responder had the needed **capability
  tags** (meaning nobody *could* go). It's tracked separately from low
  acceptance.
- **Routing priority**: the score that ranks who gets pinged first. Its
  inputs are proximity (a travel-time estimate), availability, capability
  match and recent acceptance history. Turning down or missing a ping
  lowers that history.
- **Mutual aid / shared cover**: responders covering for each other. Not
  supported yet; on the Q4 exploration list.
- Supply terms: requisition, quartermaster, field failure report, service
  interval.

### Where things stand
**Releases:** 4.0 (7 Apr: console navigation, profile redesign, routing
override audit log) · 4.1 (16 Jun: travel-time proximity, bulk callout,
push reliability) · 4.2 (12 Aug: proximity weighted up vs. acceptance
history; ping wait cut from 90s to 60s; console filters persist; three
defect fixes).

**4.2 is the live issue.** Here's what the record says, with no conclusions
drawn:
- Since the release, fewer pings are being taken and callout tickets are
  running about 3x normal. Nadia's split: roughly 2/3 say "phone never goes
  off" and 1/3 say "gone before I could answer." She ties the second group
  to the 60s ping wait. She can't explain the first.
- On 14 Aug Marcus asked whether the routing change was *meant* to apply to
  responders who have been turning jobs down. He said the config doesn't
  distinguish them. That question is still unanswered. Wen was away
  14–24 Aug and said she'd look when back.
- Priya's view: mostly seasonal ("August is always soft"), two changes
  moving at once, don't revert 4.2. On 28 Aug the team agreed to regroup
  on 4.2 once the new PM was up to speed. I found no record of that regroup
  happening. Nadia has a ticket breakdown ready.
- So far only "rough" numbers from Marcus have been mentioned. The real
  weekly numbers are Ravi's.

**Q3 roadmap** (last reviewed 30 Jun; Priya owns every item, so all of them
now need a new owner):
- Committed to 4.2: Change to who gets pinged (shipped), Ping timeout
  tuning, Availability Confidence. **Availability Confidence isn't in the
  4.2 release notes.** Priya's handoff says items were squeezed out of 4.2
  and that I need to agree with Helen which ones are still Q3 commitments.
- Committed to 4.3: Requisition approval chains (Supply).
- Exploring for Q4: Handler phone app, Shared cover between responders.
- Committed items change only through Product.

**Product briefs:**
- *Routing Override Audit Log* (Mar): small and well scoped. It shipped
  in 4.0.
- *Bulk Callout* (Jan): same callout to several responders at once. It
  shipped in 4.1, but the brief still says nobody has picked it up and
  there's no baseline for time-to-full-coverage.
- *Requisition Approval Chains* (Jul, Supply): the core ask is a second
  sign-off over $2,000. The brief then piles on scope (48h routing,
  dashboard, handler view, replacing the spreadsheet), and phasing is TBD.
- *Handler Phone App* (8 Sep): notifications, status view, one-tap
  contact. Sofia owns it for Q4 exploration. Not staffed; no baseline.

**Priya's open to-dos for me:** write down how routing decides who gets
pinged (no doc exists; talk to Wen). Settle the squeezed-out 4.2 items
with Helen. Don't let console filter-persistence tickets eat the first
month.

**Module 1 findings (cross-checked wiki, database, repo code):**
- The database (pings and tickets, 29 Jun–7 Sep) shows no August dip before 4.2. The week of 3 Aug had the best acceptance rate; the drop starts the week 4.2 shipped. Missed pings went from about 4 a week to 38.
- Four responders (Farlight, The Undertow, Vesper, Meteor Mite) fell from about 12 pings a week to about 1, and the recovering average hides them. Tickets cover Farlight and The Undertow; Vesper and Meteor Mite show up only in interviews.
- In the code (`00-rook/code/dispatch-routing`), a missed ping is penalized the same as a turned-down one (−0.12 vs +0.08 for a yes), and the score never fades back to neutral (an open TODO since 2019).
- Likely root causes (inference, unconfirmed): the shorter 60s wait led to more misses, and the miss penalty kept those responders sliding down the order. No owner or real numbers meant nobody caught it. Confirm with Wen and Ravi.
- The Requisition Approval Chains brief contradicts Halloran's interview: Halloran wants faster approvals, not a second step. The Bulk Callout and Audit Log briefs are stale (both shipped).
- The student prefers plain English, short answers and visuals. Avoid unexplained Rook jargon.

**Module 2 findings (interviews + all 147 tickets):**
- Tickets grouped: gone quiet 30, job gone mid-reach 15, other ping glitches 6, alert sound 2, saved filters 16, hard to see 8, other console 42, Supply 26, billing 2. All 45 gone-quiet and job-gone tickets came after 4.2 and are still open. Tickets went from about 6 a week to about 29.
- Before vs. after 4.2: misses went from about 4 to about 28 a week, while refusals *fell* (about 36 to about 31). The never-fading penalty existed before but was dormant.
- The two piles barely overlap: the interviewed handlers filed only 1 ticket. Tickets miss Vesper, Meteor Mite and The Gale (overloaded, about 13 to 19 a week). Interviews miss Farlight, The Undertow, Halfmoon and Corporal Ashgrove. Only the pings data covers all 16.
- Contradictions: Halloran says maintenance scheduling got smarter, but 4 tickets disagree. Saved filters sound like a win in interviews but have 12 bug tickets.
- Backlog drafted in `01-origin-story/4.2-recovery-requirements.md`: 3 initiatives, 7 epics, 22 stories, no new roadmap lines. P0 reopens "Ping timeout tuning" to fix the answer window and the miss penalty, and replies to the 45 open tickets.
- Open: Helen on Availability Confidence vs. story 3.1.2; flag the 4.3 approval-chain conflict to Supply; consider interviewing Linda Pruitt and Desmond Okafor.

**Module 3 findings (pings + callouts + tickets in rook-database; routing code):**
- All 1,696 pings saved in `03-rewind/pings-rows-used.csv`. After 4.2: % taken 76.6% → 64.0%, misses about 4 → 30 a week, turn-downs fell (36 → 30). Misses move on release day; "gone quiet" tickets lag 1–2 weeks and peak after misses had started falling.
- Groups by ping change: cut off (Farlight, The Undertow, Vesper, Meteor Mite: pings fell by half or more), fading (Corporal Ashgrove, Halfmoon), picking up (the other 10, up 16–42%). Time of day explains nothing. In every case the misses came before the drop in pings.
- In the cut-off responders' own areas, a local was asked first 80% → 17% of the time, despite 4.2 weighting distance up. Nobody ever takes jobs outside their own area; since 4.2 the busy responders get many more of these and miss most of them.
- Mechanism (inference): score = 0.60 closeness + 0.25 recent-yes + 0.15 capability. A full recent-yes score is worth about 19 minutes of travel. Break-even is 60% taken. Replaying the score: Farlight fell from 0.84 to 0 by 28 Aug; The Gale refilled to ~0.96 within days. The strongest predictor of the drop is release-week miss share (r ≈ −0.81). Behaviour before 4.2 shows no link.
- The published dashboard (claude.ai artifact "Release 4.2 Ping Drop") loads blank because rook-database only works inside this session. The student chose to use visuals in chat instead.
- Open: Wen to share real score history and travel times; answer times aren't recorded anywhere; Marcus's 14 Aug question on whether a miss should equal a refusal is still unanswered.

**Module 4 findings (routing code in `00-rook/code/dispatch-routing` + pings/callouts):**
- Correction to Module 3: before 4.2 nobody took out-of-area jobs, but after 4.2 busy responders took 86 (Captain Vantage, Sgt. Falkirk, Stormwrack 14 each; Nightwell 13). That's how outsiders took ~85% of callouts in the cut-off responders' areas.
- Code status: nothing is written-but-not-live. The trap rules (miss = no, −0.12 vs +0.08, no recovery) predate 4.0; 4.2 only changed the wait (90→60s) and weights. Never built: score recovery (2019 TODO), separate miss penalty, recording answer times, area awareness, Availability Confidence. Phone/map functions are blank outlines in this copy; bulk callout isn't in the folder.
- Marcus's 14 Aug question: the score carries pre-release history, but the 1.0 ceiling had wiped old turn-downs; post-release turn-downs didn't sink anyone (Halfmoon turned down most and recovered). Misses decided it. Intent still for Wen/Helen.
- Proposed score (Option A): taken +0.08, turned down −0.03, missed −0.05, keeping 60s. Replay: cut-off four end 0.67–0.75 instead of 0; projected 8–11 pings/wk instead of 0–1. Option B (no −0.05, miss −0.03) looks similar on paper but rewards ignoring pings. Projection model fitted to actuals, off by ~3 pings/responder/week.
- Test plan: record answer times first, full routing replay with Wen, pilot by area or alternating weeks for 4 weeks. The four already at zero need a separate reset decision.

**Recap after Module 4:**
- Correction: the cut-off four missed 44–63% of their release-week pings (71% was The Undertow's first three days only).
- Data, code and tickets agree on the order: misses first, then the drop in pings, then tickets. Still inference: the scores (my replay) and whether 4.2 was meant to work this way.
- Open, by owner: Wen (real score history, travel times, full routing replay); Wen/Ravi (record answer times, official weekly numbers); me, Helen and Marcus (should a miss count as a no?); me and Wen (reset the four at zero?); Helen (Availability Confidence); Nadia (reply to 45 open ping tickets).
