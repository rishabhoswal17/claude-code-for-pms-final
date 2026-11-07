**To** Helen Achebe · **From** Rook Dispatch PM · **Date** 7 Nov 2026 · **Re** Release 4.2, quiet responders · **Status** Draft for discussion

# Fix the engine, heal the four, end the silence

> You asked what we'd build instead, seen by the people it happens to, before anyone touches the code.

Three parts, shipped in this order. First make the routing rule fair. Then bring back the four responders it already cut off. Then make sure a responder going quiet can't stay invisible again.

**1** The engine · **2** The healing journey · **3** The silence

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

*What changes in how we rank who gets asked*

### A miss isn't a full no

| Answer | Today | Proposed |
|---|---|---|
| Taken | +0.08 | +0.08 |
| Turned down | ~~−0.12~~ | −0.03 |
| Missed | ~~−0.12~~ | −0.05 |

One bad week no longer wipes someone out.

### Scores heal: a rough patch fades on its own

Scores ease back toward neutral over time. This answers the open question in the code note from 2019.

That note's own counterpoint still holds: if someone stops taking work, that should stick. So healing is slow, and it never outruns a real pattern of no's. Wen and I set the speed.

### Saying no beats silence: no new button needed

Responders can already turn a job down or set themselves away. Under the new rule, turning down costs less than missing, and being away costs nothing, because away responders aren't asked at all.

No change to the availability feed that Rook Supply reads.

> **8–11** pings a week for the cut-off four in our replay of the new rule, instead of 0–1. The replay can be off by about 3 a week.

---

## Part 2 · The healing journey

*A fair rule protects people from now on. It doesn't lift anyone already at zero.*

| | Day 0 | Same day | Weeks 1–4 | Week 4 |
|---|---|---|---|---|
| **We do** | Reset score to neutral (0.5), same as any new responder | Send both messages below | Watch their weekly pings against their usual 12 | Check: each back to 8 or more a week? |
| **Responder** | Starts getting local offers again | "You're back in the rotation. Missed offers now count for less." | Taking jobs lifts their score as normal | Back to their usual pace |
| **Handler** | No action needed | "Farlight is back in the rotation after a quiet spell." | Coverage card shows pings returning | Quiet flag clears |

Farlight (score 0) · The Undertow (score 0) · Vesper (score 0) · Meteor Mite (score 0) · *Scores from our replay*

The reset ships on the same day as the new rule. Reset them under the old rule and they'd slide straight back.

---

## Part 3 · The silence

*Nobody could see it happening: not the responder, not the handler, not us*

### What a responder feels

**Today:** *Nothing.* Fewer offers, no explanation. Feels like being dropped.

**With this:**
> **Heads up**
> You've missed 3 offers this week, so you may get fewer for a while. Busy? Set yourself away. It won't count against you.

Only switched on after Part 1. Before that, it would just be announcing an unfair score. Wording to be tested with responders.

### What a handler sees

**Today:** *Farlight · Available.* Looks fine. The phone just never goes off.

**With this:**
> **Farlight** · `Quiet`
> 1 ping this week · usual 12
> Most likely cause: missed offers. Check in or update availability.

The card always says what to do next. Example uses Farlight's real numbers. Kip runs several responders, so each gets their own alert sound (Kip's own ask).

---

## Before we ship, we need to know

- Were misses slow answers or pings that never arrived? We record neither answer times nor delivery. — **Wen**
- Were "miss = no" and the 60s window intended, and why? Marcus asked on 14 Aug, still unanswered. — **Wen, you**
- Real score history, travel times and a healing speed. Every score above is our replay. — **Wen**
- What a quiet responder actually wants to hear. We've only interviewed handlers. — **Sofia**

## Decisions I need from you

1. Agree that a miss shouldn't count as a full "no". Direction only. Wen and I set the numbers.
2. Approve the reset for the four, shipped with the new rule.
3. Treat this as the "Ping timeout tuning" Q3 item, and decide whether the handler card replaces Availability Confidence.

---

## Next four weeks, and how we'll know it worked

Start recording answer times now. Replay routing with Wen. Talk to two responders. Click-through prototype of the Part 2 and Part 3 screens. Then pilot Parts 1 and 2 by area for four weeks.

| Measure | Target |
|---|---|
| Pings taken, back to pre-4.2 | ≥ 76.6% |
| Pings for each of the four | ≥ 8 / wk |
| New "phone never goes off" tickets | → 0 |
| Time from ping to taken | No worse |

---

*Not in this brief, parked for later: preferring local responders for local jobs, and an automatic alert when anyone's pings halve.*

*Sources: pings, callouts and tickets in the Dispatch database (29 Jun–7 Sep), the routing code, 147 support tickets and September interviews. Score figures and projections are our own replay, pending Wen's real data.*
