**To** Helen Achebe · **From** Rook Dispatch PM · **Date** 7 Nov 2026 · **Re** Release 4.2, quiet responders · **Status** Draft for discussion

# Fix the engine, heal the four, end the silence

> You asked what we'd build instead, seen by the people it happens to, before anyone touches the code.

Three parts, shipped in this order. First make the routing rule fair. Then bring back the four responders it already cut off. Then make sure a responder going quiet can't stay invisible again.

**1** The engine · **2** The healing journey · **3** The silence

**A click-through prototype goes with this brief** (`05-super-speed/prototype.html`). It has the handler console, the responder app, and a replay of 4.2 for the four responders it cut off. Everything below is on those screens.

---

## What happened

| | | |
|---|---|---|
| **90s → 60s** | 4.2 shortens the answer window | Less time to answer a job offer (a "ping"). |
| **~4 → ~30** | Missed pings a week | The four hit hardest missed 44–63% in release week. |
| **0.84 → 0** | Each miss counted as a "no" | The penalty never fades. Farlight hit zero by 28 Aug. |
| **12 → ~1** | Pings a week for the cut-off four | Their areas' jobs went to busy responders from elsewhere. |
| **45 open** | Handlers find out late | "Phone never goes off" tickets land 1–2 weeks after. |

Pings taken fell from 76.6% to 64.0%. The "miss = no" and "never fades" rules are older than 4.0. 4.2 didn't create them, it woke them up. Turn-downs actually fell. Misses decided who got cut off.

---

## Part 1 · The engine: a fair rule

*What changes in how we rank who gets asked. Scores run from 0.0 to 1.0.*

### A miss isn't a full no

| Answer | Today | Proposed |
|---|---|---|
| Taken | +0.08 | +0.08 |
| Turned down | ~~−0.12~~ | −0.03 |
| Missed | ~~−0.12~~ | −0.05 |

One bad week no longer wipes someone out.

### Scores heal: a rough patch fades on its own

Scores ease back toward 0.5 over time. This answers the open question in the code note from 2019.

The prototype uses 20% of the way back each week. That also trims high scores, so a steady responder settles near 0.9. Wen and I set the real speed.

### Saying no beats silence: Away, with a time limit

Turning down costs less than missing, and being away costs nothing, because away responders aren't asked at all.

New: setting Away asks for how long (1 hour, rest of today, or until switched back), so nobody forgets and goes quiet a new way. This changes the availability record Rook Supply reads, so Supply signs off first.

---

## Part 2 · The healing journey

*A fair rule protects people from now on. It doesn't lift anyone already at zero.*

| | Day 0 | Same day | Weeks 1–4 | Week 4 |
|---|---|---|---|---|
| **We do** | Reset score to neutral (0.5), same as any new responder | Send both messages below | Watch their weekly pings against their usual 12 | Check: each back to 8 or more a week? |
| **Responder** | Starts getting local offers again | "Welcome back. It may take a couple of weeks to get back to your usual pace." | "Your offers are picking up" | "Back to your usual pace" |
| **Handler** | Shows under "Needs a look" as Recovering | "Back in the rotation today after a quiet spell" | Offers this week climb against their usual mark | Drops off the Needs a look list |

Farlight, The Undertow, Vesper and Meteor Mite all sit at a score of 0 in our replay. The reset ships on the same day as the new rule. Reset them under the old rule and they'd slide straight back.

---

## Part 3 · The silence

*Nobody could see it happening: not the responder, not the handler, not us*

### What a responder sees

**Today:** *Nothing.* Fewer offers, no explanation. Feels like being dropped.

**With this:**
> **You've missed a few offers**
> 3 this week. If you can't take one, tap Turn down, or set yourself Away when you're busy. That keeps offers coming your way. `[Set Away for today]`

- **Their score, 0.0 to 1.0**, with a what-if: tap take (+0.08), turn down (−0.03) or miss (−0.05) and see where it lands. The ranking and the other inputs stay hidden.
- **Offers take over the screen**, with a 60-second ring and "Why you: closest available, 6 min away."
- **This week**: offers against their usual week, the last 6 weeks in neutral colours, and "No answer" instead of a red "Missed".

Score and heads-up only switch on after Part 1. Before that they'd just be announcing an unfair score. Wording to be tested with responders.

### What a handler sees

**Today:** *Farlight · Available.* Looks fine. The phone just never goes off.

**With this:**
> **Farlight** · `Recovering`
> Offers coming back: 7 this week · usual 12
> Last offer: today 09:15 · Avg trip `6 min`

- **One Coverage list**, with "Needs a look" first: Quiet, Recovering, Missing offers, Busy. Day and Week change the numbers, not the layout.
- **Last offer** turns red after 3 days. **Busy** shows the offers above usual in amber.
- **Check in** sends a message the responder can answer in one tap. **Callouts** has its own page: who was asked, who took it, how far away.

Distance is shown in minutes only, never as a map of where a responder is. These are masked responders, and Security Policy 4.1 rules out working out who someone is. Example uses Farlight's real numbers.

---

## What the replay shows

Real pings to 6 Sep from the saved data, then 4 projected weeks. The "with fix" columns assume the fair rule, healing, and half of missed offers turning into a "no" after the heads-up.

| Responder | Usual week | Real, wk of 31 Aug | No fix, wk of 28 Sep | Fix, habits recover over 8 wks | Fix, habits never recover |
|---|---|---|---|---|---|
| Farlight | 12 | 0 | 0 | 12 · score 0.90 | 4 · score 0.25 |
| The Undertow | 12 | 1 | 0 | 12 · score 0.90 | 5 · score 0.29 |
| Vesper | 14 | 1 | 0 | 14 · score 0.90 | 10 · score 0.48 |
| Meteor Mite | 11 | 1 | 0 | 11 · score 0.90 | 5 · score 0.32 |

> **The rule stops the damage. Answering habits decide the recovery.** After 4.2 these four missed 53–64% of offers. If that doesn't change, even the fair rule lets their scores drift down. That's why the heads-up, Turn down and Away matter as much as the rule, and why we need answer times recorded. This replaces the earlier "8–11 pings a week" estimate, which only re-scored the pings they actually got.

---

## Before we ship, we need to know

- Were misses slow answers or pings that never arrived? We record neither answer times nor delivery. — **Wen**
- Were "miss = no" and the 60s window intended, and why? Marcus asked on 14 Aug, still unanswered. — **Wen, you**
- Real score history, travel times and a healing speed. Every score and distance above is our replay or an estimate. — **Wen**
- How fast answering habits recover. The biggest driver in the replay, and a guess today. — **Ravi, Sofia**
- What a quiet responder wants to hear and see, including their score. We've only interviewed handlers. — **Sofia**
- Away with a time limit. It changes the availability record Supply reads. — **Supply**

## Decisions I need from you

1. Agree that a miss shouldn't count as a full "no". Direction only. Wen and I set the numbers.
2. Approve the reset for the four, shipped with the new rule.
3. Agree to show responders their own score with the what-if. Never the ranking or the other inputs.
4. Treat this as the "Ping timeout tuning" Q3 item, and decide whether the handler's Coverage list replaces Availability Confidence.

---

## Next four weeks, and how we'll know it worked

Start recording answer times now. Replay routing with Wen on real scores. Test the prototype with two responders and two handlers. Then pilot Parts 1 and 2 by area for four weeks.

| Measure | Target |
|---|---|
| Pings taken, back to pre-4.2 | ≥ 76.6% |
| Pings for each of the four | ≥ 8 / wk |
| Offers missed by the four (pre-4.2: 1–4%) | ≤ 10% |
| New "phone never goes off" tickets | → 0 |
| Time from ping to taken | No worse |

---

*Not in this brief, parked for later: changing routing to prefer local responders for local jobs. Distance is shown, but it doesn't change who gets asked.*

*Sources: pings, callouts and tickets in the Dispatch database (29 Jun–7 Sep), the routing code, 147 support tickets and September interviews. Scores are replayed from the saved ping data starting at 0.5 on 29 Jun. Everything after 6 Sep is projection. The prototype's roster, callouts and trip times are illustrative.*
