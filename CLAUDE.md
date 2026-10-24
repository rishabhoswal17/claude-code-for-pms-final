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
