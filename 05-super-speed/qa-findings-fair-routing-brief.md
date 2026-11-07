# QA findings: Fair Routing brief

| | |
|---|---|
| **Brief tested** | `05-super-speed/brief.md` (Fair Routing brief, draft of 7 Nov 2026) |
| **Build tested** | `05-super-speed/prototype.html`, treated as the staging build |
| **Date** | 7 Nov 2026 |
| **Browser** | Built-in browser at desktop width (1280 × 900) and phone width (375 × 812) |
| **Status** | **Tested; both Major issues fixed and re-tested** |

## Verdict

The prototype matches the brief closely, with no blockers. The first run found two Major issues: Farlight's August numbers differed between two screens, and the score shown in the app didn't follow the rule the brief proposes. Both are now fixed in `prototype.html` (and its copy `prototype-all-changes.html`) and re-tested. What's left is minor.

| | Pass | Fail | Partly | Blocked | Not testable here |
|---|---|---|---|---|---|
| First run | 43 | 2 | 5 | 1 | 9 |
| After fixes | 46 | 1 | 3 | 1 | 9 |

## Re-test after fixes (7 Nov 2026)

| Issue | Fix | Re-test |
|---|---|---|
| Top issue 1 (AC-4.10) | The console chart for Farlight and The Undertow now uses the real weekly pings for 3–31 Aug, the same data as the replay. | Farlight: 12, 10, 3, 1, 0 on both screens. The Undertow: 12, 11, 4, 1, 1 on both. **Pass** |
| Top issue 2 (AC-1.6, AC-1.7) | Farlight's score is now worked out from the fair rule: reset to 0.5 on Day 0, each week's answers added, then 20% healing at week end. The week of 9 Nov is assumed to be 4 taken and 1 turned down. Live clicks now cap at 0 and 1 after every single answer. | Day 0: 0.50. One live miss: 0.45. Weeks 2–4 start at 0.73, 0.90 and 0.90, and reach 1.00 with that week's answers. Week 4 with 3 misses: 1.00 → 0.85. No console errors. **Pass** |

## Top issues (first run)

**1. Major (fixed): Farlight's August numbers differ between the handler console and the replay (AC-4.10)**
- *Expected:* the brief says the example "uses Farlight's real numbers", so every screen should show the same weekly offers.
- *Actual:* the handler console's "Offers per week" chart shows 13, 9, 4, 2, 1 for the weeks of 3–31 Aug. The replay, built from the saved ping data, shows 12, 10, 3, 1, 0 for the same weeks. The footer says Farlight's numbers come "from our analysis", so the console chart reads as real when it isn't.
- *Steps:* Handler console → Week 2 → click Farlight → hover the bars under "Offers per week". Then open 4.2 replay → Farlight → hover the same weeks.

**2. Major (fixed): the score in the app doesn't follow the proposed rule (AC-1.6, AC-1.7)**
- *Expected:* the score goes up 0.08 for each offer taken and down 0.03 for each one turned down, then moves 20% of the way back to 0.5 each week.
- *Actual:* Farlight's score reads 0.50 (Day 0), 0.65 (Week 2), 0.71 (Week 3) and 0.76 (Week 4). Under the rule, Week 2 alone (6 taken, 1 turned down) adds about 0.45, so Farlight would be near 0.9 by Week 3. The live taps do follow the rule (one miss 0.50 → 0.45; three misses 0.76 → 0.61); only the starting score for each week is off. A responder who tries the what-if against their own week would find it doesn't add up, which undermines the point of showing the score.
- *Steps:* Responder app → This week → step through Day 0, Week 2, Week 3 and Week 4 and compare the score with that week's taken and turned-down counts.

**3. Minor: "Recovering" ends by date, not when offers come back (AC-2.9)**
- *Expected (gap G4):* a reset responder stays on "Needs a look" until they reach 8 offers a week.
- *Actual:* the build only tags someone "Recovering" up to Week 2. From Week 3 on, a reset responder with 6–7 offers would show as normal and leave the list. The demo data can't produce this case, so I found it by reading the build's code.

**4. Minor: mixed messages after missed offers in Week 4**
- *Actual:* after "Simulate 3 missed offers" in Week 4, the app shows "You've missed a few offers" directly above "Back to your usual pace… Nice work", and the summary at the top still says "Right around your usual".
- *Steps:* Responder app → Week 4 → Simulate 3 missed offers.

## Results

### 1. The fair rule (brief Part 1)

| ID | Criterion | From the brief | Check | Result | What we saw |
|---|---|---|---|---|---|
| AC-1.1 | Taking an offer raises the score by 0.08. | "Taken +0.08" | Build | Pass | What-if: 0.50 → 0.58. |
| AC-1.2 | Turning down lowers it by 0.03. | "Turned down −0.03" | Build | Pass | What-if: 0.58 → 0.55. |
| AC-1.3 | A miss lowers it by 0.05. | "Missed −0.05" | Build | Pass | What-if: 0.55 → 0.50. A real timed-out offer: 0.50 → 0.45. Three misses: 0.76 → 0.61. |
| AC-1.4 | The score stays between 0.0 and 1.0. | "0.0 to 1.0" | Build | Pass | The build caps each step at 0 and 1. Checked in its code; not pushed to the limit by clicking. |
| AC-1.5 | The old −0.12 isn't shown as the current rule. | "~~−0.12~~" | Build | Pass | −0.12 only appears in the replay's "no fix" comparison. |
| AC-1.6 | The score moves 20% of the way back to 0.5 each week. | "20% … each week" | Build | Pass (after fix) | First run: Partly; the app's weekly scores didn't follow the rule. Now 1.00 at week end heals to 0.90 the next week, the same rule as the replay. |
| AC-1.7 | A steady responder settles near 0.9. | "settles near 0.9" | Build | Pass (after fix) | The replay ends at 0.90 for all four. The app now starts Weeks 3 and 4 at 0.90. |
| AC-1.8 | Away asks how long: 1 hour, rest of today, or until switched back. | "asks for how long" | Build | Pass | Sheet offers "For 1 hour", "For the rest of today", "Until I switch back". |
| AC-1.9 | While Away, no offers and no score change. | "being away costs nothing" | Build | Pass | Sent an offer while Away: it went to Nightwell ("Farlight away, not asked"). Score stayed 0.45. |
| AC-1.10 | Away ends on its own when time runs out. | "so nobody forgets" | Build | Blocked | The prototype has no clock, so a timer can't run out. |

### 2. Bringing back the four (brief Part 2)

| ID | Criterion | From the brief | Check | Result | What we saw |
|---|---|---|---|---|---|
| AC-2.1 | The four are reset to 0.5. | "Reset score to neutral (0.5)" | Build | Partly | Farlight shows 0.50 on Day 0. The Undertow is tagged Recovering, but handlers never see scores. Vesper and Meteor Mite aren't in the prototype at all, and the replay models "4.2 shipped with the fix", not a reset. |
| AC-2.2 | The reset comes with the new rule, never without it. | "same day as the new rule" | Build | Pass | The Day 0 timeline step switches on the rule, the reset and the new screens together. |
| AC-2.3 | Day 0 responder message. | Part 2 table | Build | Pass | "Welcome back. You'll start getting offers again from today. It may take a couple of weeks to get back to your usual pace." |
| AC-2.4 | Weeks 1–4: "Your offers are picking up". | Part 2 table | Build | Pass | Week 2: "Your offers are picking up. 7 this week, up from 5 last week." Week 3 says "Nearly back to your usual pace". |
| AC-2.5 | Back to 8+: "Back to your usual pace". | Part 2 table | Build | Pass | Week 4: "Back to your usual pace. 10 offers this week." |
| AC-2.6 | Handler sees the reset responder under "Needs a look", tagged Recovering. | Part 2 table | Build | Pass | Day 0: The Undertow under Needs a look, Recovering, "Back in the rotation today after a quiet spell". |
| AC-2.7 | Handler sees this week's offers against usual. | "climb against their usual mark" | Build | Pass | "Offers coming back: 7 this week, usual 12"; Week view shows "7 / 12" with a usual tick. |
| AC-2.8 | Drops off "Needs a look" at 8+ a week. | "Drops off the Needs a look list" | Build | Pass | Week 3: Farlight (9) and The Undertow (8) both under "Everyone else". |
| AC-2.9 | Still under 8 at week 4 → stays on "Needs a look". | Gap G4 | Build | Fail (Minor) | Recovering ends after Week 2 regardless of offers (Top issue 3). Found in the code. |

### 3. What a responder sees (brief Part 3)

| ID | Criterion | From the brief | Check | Result | What we saw |
|---|---|---|---|---|---|
| AC-3.1 | Missed offers → "You've missed a few offers" with count and advice. | "3 this week…" | Build | Partly | The message and wording match. It only appears after 3 misses: one miss on Day 0 showed nothing. That fails my reading of gap G1 (1 or more), but matches the brief's own example. |
| AC-3.2 | "Set Away for today" sets them Away for today. | "[Set Away for today]" | Build | Pass | Chip changes to "Away · today"; "You're Away until tomorrow. It won't count against you." |
| AC-3.3 | Score shown on a 0.0–1.0 scale. | "0.0 to 1.0" | Build | Pass | "0.50 out of 1.0 · 0.5 is where everyone starts", with a meter. |
| AC-3.4 | What-if shows where the score lands; the real score doesn't move. | "with a what-if" | Build | Pass | Take, No, Miss → 0.50 (+0.00). The big score stayed 0.50 throughout. |
| AC-3.5 | Never shows ranking, other scores or other inputs. | "stay hidden" | Build | Pass | Only their own score, plus "A higher score means you're asked sooner when you're one of the closest responders." |
| AC-3.6 | An offer fills the screen with a 60-second ring. | "60-second ring" | Build | Pass | Full-screen offer with a 60-second ring (runs at 10× speed in the demo). |
| AC-3.7 | Offer says why them. | "Why you: …" | Build | Pass | "Why you: you're the closest available responder, 6 min away, with first aid and climbing." |
| AC-3.8 | Time runs out → offer closes, shows "No answer". | 60s window | Build | Pass | "No answer in time. It's gone to someone else." This week: "1 no answer". |
| AC-3.9 | "This week" shows offers vs usual, and the last 6 weeks. | "This week…" | Build | Pass | "7 · usual 12 · Building back up"; 6-week chart with a "usual 12" line. |
| AC-3.10 | No red "Missed"; neutral "No answer". | "instead of a red 'Missed'" | Build | Pass | The new app says "No answer" in grey. The word "Missed" doesn't appear on the phone. |
| AC-3.11 | Score and message are off without the new rule. | "only switch on after Part 1" | Build | Pass | "Before the fix" has no score, no message and no Simulate button. There's also a "Score on app" switch. |
| AC-3.12 | Fits a 375px phone, no sideways scroll, all buttons tappable. | Phone app | Build | Pass | Page width stayed 375px. Take it and Turn down sit inside the phone at 54px tall. |

### 4. What a handler sees (brief Part 3)

| ID | Criterion | From the brief | Check | Result | What we saw |
|---|---|---|---|---|---|
| AC-4.1 | Farlight card: Recovering, 7 this week · usual 12, last offer, 6 min trip. | Farlight example | Build | Pass | Week 2: Recovering, "Offers coming back: 7 this week, usual 12", "Today 09:15", "6 min". Matches the brief exactly. |
| AC-4.2 | One Coverage list, "Needs a look" first, with the four statuses. | "One Coverage list…" | Build | Pass | One list: "Needs a look", then "Everyone else". Missing offers, Recovering and Busy all appear; no one is Quiet in the demo data, so that one was only checked in the code. Order is Missing offers → Quiet → Recovering → Busy, a different order from the brief's list. |
| AC-4.3 | Day/Week changes numbers, not layout. | "not the layout" | Build | Pass | Week 3: same groups and rows; "Offers today 5" becomes "Offers this week 12 / 12". |
| AC-4.4 | "Last offer" red after 3 days, not before. | "red after 3 days" | Build | Partly | Red at 8 and 6 days ago; "Yesterday" and "Today" stay dark. The code turns red at exactly 3 days, not after 3 full days (gap G3). The demo data has no 3-day case. |
| AC-4.5 | Busy shows offers above usual in amber. | "in amber" | Build | Pass | Week 2, The Gale 17 / 13: the extra part of the bar is amber, with a Busy pill. |
| AC-4.6 | "Check in" reaches the responder; one-tap reply. | "Check in sends a message…" | Build | Pass | "Checking in" arrived with "All good" and "Busy this week". Tapped "All good" and the reply was sent. |
| AC-4.7 | Callouts page: who was asked, who took it, how far. | "Callouts has its own page" | Build | Pass | Time · Callout · Asked (+ minutes, outcome) · Taken by (+ minutes). Only the first person asked is shown, not each one in turn. |
| AC-4.8 | Minutes only; no map or location. | "never as a map" | Build | Pass | Distances are "N min" chips. The offer has a simple "You — 6 min" line. No map, address, coordinates, images or embeds anywhere. |
| AC-4.9 | No legal names or identity. | "Security Policy 4.1" | Build | Pass | Only responder names; the handler is "Signed in as handler". |
| AC-4.10 | Farlight's numbers match on every screen. | "Farlight's real numbers" | Build | Pass (after fix) | First run: Fail (Major); the August history didn't match the replay. Now the console, the app and the replay all show the same numbers. |

### 5. The 4.2 replay

| ID | Criterion | From the brief | Check | Result | What we saw |
|---|---|---|---|---|---|
| AC-5.1 | Usual weeks 12, 12, 14, 11. | Replay table | Build | Pass | 12, 12, 14, 11. |
| AC-5.2 | Real week of 31 Aug: 0, 1, 1, 1. | Replay table | Build | Pass | 0, 1, 1, 1. |
| AC-5.3 | No fix, week of 28 Sep: all 0. | Replay table | Build | Pass | All 0, score 0.00. |
| AC-5.4 | Habits recover over 8 weeks: 12, 12, 14, 11, score 0.90. | Replay table | Build | Pass | 12, 12, 14, 11, all 0.90 (default settings). |
| AC-5.5 | Habits never recover: 4, 5, 10, 5; scores 0.25, 0.29, 0.48, 0.32. | Replay table | Build | Pass | Exact match after choosing "Never". |
| AC-5.6 | Real data marked apart from projection. | "after 6 Sep is projection" | Build | Pass | Shaded "next 4 weeks, projected" area; tooltips say "(projected)". |
| AC-5.7 | States its assumptions. | "The 'with fix' columns assume…" | Build | Pass | "How this works" and "Assumptions" notes: 20% healing, 0.5 start, 50% slider for misses becoming a "no". |

### 6. Across the whole build

| ID | Criterion | From the brief | Check | Result | What we saw |
|---|---|---|---|---|---|
| AC-6.1 | Nothing claims local-first routing. | "parked for later" | Build | Pass | Distance is shown, and "jobs outside their area" is only a label. |
| AC-6.2 | No browser console errors. | Basic | Build | Pass | No console messages at load or after any of the clicks above. |
| AC-6.3 | Says the data is illustrative. | "illustrative" | Build | Pass | "Example data · not live" badge, and a footer naming what's illustrative. |

## Not testable in this build

| ID | What needs checking | Who can check |
|---|---|---|
| AC-N.1 | Answer times are recorded for every ping. | Wen, Ravi |
| AC-N.2 | Whether misses were slow answers or pings that never arrived. | Wen |
| AC-N.3 | Real score history, travel times and the right healing speed. | Wen |
| AC-N.4 | The live routing really skips responders who are Away. | Wen |
| AC-N.5 | Supply signs off on Away time limits. | Supply |
| AC-N.6 | How fast answering habits recover. | Ravi, Sofia |
| AC-N.7 | Responders understand the wording and want to see their score. | Sofia |
| AC-N.8 | The pilot hits its targets: ≥ 76.6% taken, ≥ 8 offers a week for each of the four, ≤ 10% of their offers missed, new "phone never goes off" tickets → 0, and time from ping to taken no worse. | Ravi (pilot) |
| AC-N.9 | Helen's four decisions in the brief. | Helen |

## Gaps in the brief

| # | Gap | Reading used | What the build does | Question to settle it |
|---|---|---|---|---|
| G1 | How many misses trigger "You've missed a few offers". | 1 or more | 3 or more, which matches the brief's example | Suggest writing "3 in a week" into the brief. |
| G2 | No thresholds for Quiet, Missing offers or Busy. | Accept the build's if consistent | Quiet: under half of usual. Busy: over 1.3× usual. Missing offers: 3+ misses. | Agree these numbers with Sofia and Nadia. |
| G3 | "Red after 3 days": at 3 or after 3? | After 3 full days | At exactly 3 days | Which one? |
| G4 | Not back to 8 by week 4. | Stays on "Needs a look" | Leaves the list after Week 2 if offers are 6+ | What happens to someone who doesn't recover? |
| G5 | "Until switched back" can bring back the forgetting problem. | Test as written | Option exists, with no reminder | Keep it, cap it, or add a reminder? |
| G6 | Does the what-if include healing? | No healing | No healing | Fine as is, unless Sofia's interviews say otherwise. |
| G7 | Healing weekly or bit by bit? | Weekly | Weekly (replay only) | Settle with Wen. |
| G8 | Score precision. | Two decimals | Two decimals | No change needed. |

## Other issues found

| # | Severity | Issue | Where |
|---|---|---|---|
| O1 | Minor | Mixed messages: "You've missed a few offers" sits above "Back to your usual pace… Nice work" (Top issue 4). | Responder app, Week 4, after Simulate 3 missed offers |
| O2 | Minor | "Most of your offers this week were within 10 min of you" shows when there were 0 offers. | Responder app → This week, Day 0 |
| O3 | Minor | Once a responder with missed offers sets Away, the handler's "Missing offers" flag disappears and they move to "Everyone else". The handler loses the warning. | Handler console, Week 4, after missed offers + Set Away |
| O4 | Minor | Tooltips say "1 offers" and "1 pings". | Handler chart, replay chart |
| O6 | Note (for Wen and Helen) | Found while fixing Top issue 2: under the proposed numbers, one good week fills the score. With about 10 offers a week, +0.08 per offer taken reaches 1.00 within a week, and healing only trims it to 0.90. A steady responder then sees "Take one +0.00" in the what-if, and the score can't tell a good week from a great one. Worth raising when the real numbers are set. | The rule itself, not the build |
| O5 | Note | At phone width the presenter controls push the phone well down the page, so a new offer opens below the fold. This only affects the demo, not the product. | Whole page at 375px |
